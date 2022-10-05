# Интеграция сервиса для получения данных профиля пользователя.
Отчет по лабораторной работе #2 выполнил(а):
- Касьянов Никита Андреевич
- ХИ41
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Задание 2.
- Задание 3.
- Выводы.
- ✨Magic ✨

## Цель работы
Cоздание интерактивного приложения и изучение принципов интеграции в него игровых сервисов.
## Задание 1
### По теме видео практических работ 1-5 повторить реализацию игры на Unity. Привести описание выполненных действий.
Ход работы:
  Просмотрев видеоматериалы, я начал повторять последовательность приведённых действий/
-
-
-dscdc
scsdcc
    - Создал новый 3D-проект [[1]]()
    - Ознакомился с сайтом заготовленных ассетов "Unity Asset Store" и, с его помощью, добавил в свой проект модели драконов и огненные эффекты. [[2]]() [[3]]()
    
    - C помощью драконов, сфер и плоскостей создал сцену, аналогичную сцене из обучающего видео, видоизменив оттенки. Также, создал DragonEgg, Energy Shield и несколько новых материалов. [[4]]()
    - Добавил анимационный контроллер дракону, попросив его летать в пространстве при старте сцены.  [[5]]() [[6]]()
    - Повторил скрипт из видео, позволяющий дракону перемещаться по сцене из стороны в сторону с неким элементом случайности
    
```c#

public class EnemyDragon : MonoBehaviour
{
    public GameObject dragonEggPrefab;
    public float speed = 1;
    public float timeBetweenEggDrops = 1f;
    public float leftRightDistance = 10f;
    public float chanceDirection = 0.1f;
    // Start is called before the first frame update
    void Start()
    {
        Invoke("DropEgg", 2f);
    }

    void DropEgg(){
        Vector3 myVector = new Vector3(0.0f, 5.0f, 0.0f);
        GameObject egg = Instantiate<GameObject>(dragonEggPrefab);
        egg.transform.position = transform.position + myVector;
        Invoke("DropEgg", timeBetweenEggDrops);
    }
    // Update is called once per frame
    void Update()
    {
        Vector3 pos = transform.position;
        pos.x += speed * Time.deltaTime;
        transform.position = pos;

        if(pos.x < -leftRightDistance){
            speed = Mathf.Abs(speed);
        }
        else if (pos.x > leftRightDistance){
            speed = -Mathf.Abs(speed);
        }
    }

    private void FixedUpdate() {
        if( Random.value < chanceDirection){
            speed *= -1;
        }
    }
}

```

## Задание 2
### Что произойдёт с координатами объекта, если он перестанет быть дочерним? Создайте три различных примера работы компонента RigidBody.



## Задание 3
### Реализуйте на сцене генерацию n кубиков. Число n вводится пользователем после старта сцены.



## Выводы

Абзац умных слов о том, что было сделано и что было узнано.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
