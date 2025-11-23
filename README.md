# Django Səsvermə Tətbiqi (Tutorial 5)

Bu layihə, Django-nun rəsmi sənədlərindəki 5-ci tutorial olan "Automated Testing" (Avtomatlaşdırılmış Testlər) mövzusunu əhatə edən bir səsvermə tətbiqidir. Layihə, Django ilə testlərin necə yazılacağını və tətbiqin funksionallığını necə yoxlamaq lazım olduğunu praktiki şəkildə göstərir.

## Layihənin Strukturu

Layihə aşağıdakı struktura malikdir:

```
/mysite
|-- manage.py
|-- mysite/
|   |-- __init__.py
|   |-- settings.py
|   |-- urls.py
|   |-- wsgi.py
|-- polls/
|   |-- __init__.py
|   |-- admin.py
|   |-- apps.py
|   |-- migrations/
|   |-- models.py
|   |-- templates/
|   |   `-- polls/
|   |       |-- detail.html
|   |       |-- index.html
|   |       `-- results.html
|   |-- tests.py
|   |-- urls.py
|   `-- views.py
`-- README.md
```

- **mysite/**: Django layihəsinin əsas konfiqurasiya qovluğu.
- **polls/**: Səsvermə tətbiqinin yerləşdiyi qovluq.
- **polls/models.py**: `Question` və `Choice` modellərinin tərifi.
- **polls/views.py**: Tətbiqin görünüşlərinin (views) məntiqi.
- **polls/urls.py**: Tətbiqə aid URL yönləndirmələri.
- **polls/templates/**: HTML şablonlarının saxlandığı qovluq.
- **polls/tests.py**: Tətbiqin avtomatlaşdırılmış testlərinin yerləşdiyi fayl. Bu layihənin əsas fokus nöqtəsi bu fayldır.
- **polls/admin.py**: Modellərin admin panelində qeydiyyatı və konfiqurasiyası.

## Quraşdırma və İşə Salma

Layihəni lokal maşınınızda işə salmaq üçün aşağıdakı addımları izləyin:

1.  **Virtual Mühit Yaradın və Aktivləşdirin:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```

2.  **Tələb Olunan Kitabxanaları Yükləyin:**

    Layihə qovluğunda bir `requirements.txt` faylı yaradıb aşağıdakı məzmunu əlavə edin:

    ```
    Django>=5.0
    ```

    Daha sonra bu əmri icra edin:

    ```bash
    pip install -r requirements.txt
    ```

3.  **Miqrasiyaları Tətbiq Edin:**

    Verilənlər bazası cədvəllərini yaratmaq üçün:

    ```bash
    python manage.py migrate
    ```

4.  **Development Server-i İşə Salın:**

    ```bash
    python manage.py runserver
    ```

    Server işə düşdükdən sonra `http://127.0.0.1:8000/polls/` ünvanına daxil olaraq tətbiqi görə bilərsiniz.

## Testlərin İcra Edilməsi

Bu layihənin əsas məqsədi olan avtomatlaşdırılmış testləri yoxlamaq üçün aşağıdakı əmri icra edin:

```bash
python manage.py test polls
```

Bu əmr `polls/tests.py` faylındakı bütün testləri işə salacaq və nəticələri göstərəcək. Testlər aşağıdakı məsələləri yoxlayır:

- **Model Testləri (`QuestionModelTests`):**
    - Gələcək tarixdə dərc olunmuş sualların `was_published_recently()` metodunun `False` qaytarması.
    - Köhnə sualların `was_published_recently()` metodunun `False` qaytarması.
    - Yaxın zamanda dərc olunmuş sualların `was_published_recently()` metodunun `True` qaytarması.

- **View Testləri (`QuestionIndexViewTests`, `QuestionDetailViewTests`):**
    - Heç bir sual olmadıqda ana səhifədə müvafiq mesajın göstərilməsi.
    - Gələcək tarixdəki sualların ana səhifədə göstərilməməsi.
    - Keçmişdəki sualların ana səhifədə göstərilməsi.
    - Gələcək və keçmiş suallar birlikdə olduqda yalnız keçmişdəkilərin göstərilməsi.
    - Birdən çox keçmiş sualın düzgün sıralanması.
    - Gələcək tarixdəki bir sualın detallarına baxmağa cəhd etdikdə 404 xətasının alınması.
    - Keçmişdəki bir sualın detallarının düzgün göstərilməsi.

## İstifadə

- **Admin Paneli:** Yeni suallar və seçimlər əlavə etmək üçün admin paneldən istifadə edə bilərsiniz. Bunun üçün ilk öncə bir superuser yaratmalısınız:

  ```bash
  python manage.py createsuperuser
  ```

  Daha sonra `http://127.0.0.1:8000/admin/` ünvanına daxil olaraq suallar yarada bilərsiniz.

- **Səsvermə:** `http://127.0.0.1:8000/polls/` ünvanında aktiv sualları görə və səs verə bilərsiniz.
