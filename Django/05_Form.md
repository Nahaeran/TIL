# 개요
    
HTML ‘form’

: 지금까지 사용자로부터 데이터를 받기 위해 활용한 방법

그러나 비정상적 혹은 악의적인 요청을 필터링 할 수 없음

→ 유효한 데이터인지에 대한 확인이 필요

- 유효성 검사 : 수집한 데이터가 정확하고 유효한지 확인하는 과정
- 유효성 검사 구현
    - 유효성 검사를 구현하기 위해서는 입력 값, 형식, 중복, 범위, 보안 등 많은 것들을 고려해야 함
    - 이런 과정과 기능을 직접 개발하는 것이 아닌 Django가 제공하는 Form을 사용
# Django Form
    
### Form Class

Django Form

: 사용자 입력 데이터를 수집하고, 처리 및 유효성 검사를 수행하기 위한 도구

→ 유효성 검사를 단순화하고 자동화 할 수 있는 기능을 제공

```python
# Form class 정의

# articles/forms.py

from Django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField()
```

```python
# Form class를 적용한 new 로직
# articles/views.py

from .forms import ArticleForm

def new(request):
    form = ArticleForm()
    context = {
        'form' : form,
    }
    return render(request, 'article/new.html', context)
```

```html
<!-- articles/new.html -->

<h1>NEW</h1>
<form action="{% url 'articles:create %}" method="POST">
    {% csrf token %}
    {{ form }}
    <input type="submit">
</form>
```

### Form rendering options

label, input 쌍을 특정 HTML 태그로 감싸는 옵션

```html
<!-- articles/new.html -->

<h1>NEW</h1>
<form action="{% url 'articles:create %}" method="POST">
    {% csrf token %}
    {{ form.as_p }} <!--p 태그로 감싸짐 -->
    <input type="submit">
</form>
```

### Widgets

HTML ‘input’ element의 표현을 담당

[https://docs.djangoproject.com/en/4.2/ref/forms/widgets/](https://docs.djangoproject.com/en/4.2/ref/forms/widgets/)

# Django ModelForm
    
**Form**

: 사용자 입력 데이터를 DB에 저장하지 않을 때 (ex. 로그인)

**ModelForm**

: 사용자 입력 데이터를 DB에 저장해야 할 때 (ex. 게시글, 회원가입)

---

### ModelForm

Model과 연결된 Form을 자동으로 생성해주는 기능을 제공

→ Form + Model

```python
# ModelForm class 정의
# articles/forms.py

from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = '__all__'
```

- Meta class : ModelForm의 정보를 작성하는 곳
- `fields` 및 `exclude` 속성
    - exclude 속성을 사용하여 모델에서 포함하지 않을 필드를 지정할 수도 있음
        
        
        ```python
        # articles/forms.py
        
        class ArticleForm(forms.ModelForm):
            class Meta:
                model = Article
                fields = ('title',)
        ```
        
        ```python
        # articles/forms.py
        
        class ArticleForm(forms.ModelForm):
            class Meta:
                model = Article
                exclude = ('title',)
        ```
        

- Model Form을 적용한 `create` 로직
    
    ```python
    # articles/views.py
    
    from .forms import ArticleForm
    
    def create(request):
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk)
        context = {
            'form' : form,
        }
        return render(request, 'articles/new.html', context)
    ```
    
    - `is_valid()`
        - 여러 유효성 검사를 실행하고, 데이터가 유효한지 여부를 Boolean으로 반환
            
            [https://docs.djangoproject.com/en/4.2/ref/validators/](https://docs.djangoproject.com/en/4.2/ref/validators/)
            
- 공백 데이터가 유효하지 않은 이유와 에러메시지가 출력되는 과정
    - 별도로 명시하지 않았지만 모델 필드에는 기본적으로 빈 값은 허용하지 않는 제약조건이 설정 되어있음
    - 빈 값은 `is_valid()`에 의해 False로 평가되고 form  객체에는 그에 맞는 에러 메시지가 포함되어 다음 코드로 진행됨

- ModelForm을 적용한 `edit` 로직
    
    
    ```python
    # articles/views.py
    
    def edit(request, pk):
        article = Article.objects.get(pk=pk)
        form = ArticleForm(instance=article)
        context = {
            'aritcle' : article,
            'form' : form,
        }
        return render(request, 'articles/edit.html', context)
    ```
    
    ```html
    <!-- articles/edit.html -->
    
    <h1>EDIT</h1>
    <form action="{% url 'articles:update' article.pk %}" method="POST">
        {% csrf_tocken %}
        {{ form.as_p }}
        <input type="submit">
    </form>
    ```
    
- ModelForm을 적용한 `update` 로직
    
    ```python
    # articles/views.py
    
    def update(request, pk):
        article = Article.objects.get(pk=pk)
        form = ArticleForm(request.POST, instance=article)
        if form.is_valud():
            form.save()
            return redirect('articles:detail', article.pk)
        context = {
            'form' : form,
        }
        return render(request, 'articles/edit.html', context)
    ```
    

- `save()` 메서드가 생성과 수정을 구분하는 방법
    - 키워드 인자 `instance` 여부를 통해 생성할 지, 수정할 지를 결정
    
    ```python
    # CREATE
    form = ArticleForm(request.POST)
    form.save()
    
    # UPDATE
    form = ArticleForm(request.POST, instance=article)
    form.save()
    ```
    

- Django Form 정리
    
    > 사용자로부터 데이터를 수집하고 처리하기 위한 강력하고 유연한 도구
    HTML form의 생성, 데이터 유효성 검사 및 처리를 쉽게 할 수 있도록 도움
    > 

- 참고
    - Widget 응용
        
        ```python
        # articles/forms.py
        
        class ArticleForm(forms.ModelForm):
            title = forms.CharField(
                label='제목',
                widget=forms.TextInput(
                    attrs={
                        'class': 'my-title',
                        'placeholder': 'Enter the title',
                    }
                ),
            )
            
            class Meta:
                model = Article
                fields = '__all__'
        ```
            
# Handling HTTP requests
- new & create view 함수간 공통점과 차이점
    
    공통점 : 데이터 생성을 구현하기 위함
    
    차이점 : new는 GET method 요청만을, create는 POST method 요청만을 처리
    
    ∴ new와 create함수를 하나로 합치자!
    
    ```python
    def create(request):
        if request.method == 'POST':
            form = ArticleForm(request.POST)
            if form.is_valid():
                article = form.save()
                return redirect('articles:detail', article.pk)
        else:
            form = ArticleForm()
        context = {
            'form': form,
        }
        return render(request, 'articles/new.html', context)
    ```
    

- edit과 update 함수도 마찬가지!
    
    ```python
    # articles/views.py
    
    def update(request, pk):
        article = Article.objects.get(pk=pk)
        if request.method == 'POST':
            form = ArticleForm(request.POST, instance=article)
            if form.is_valid():
                form.save()
                return redirect('articles:detail', article.pk)
        else:
            form = ArticleForm(instance=article)
        context = {
            'article': article,
            'form': form,
        }
        return render(request, 'articles/update.html', context)
    ```