# Интеграция сервиса для получения данных профиля пользователя.
Отчет по лабораторной работе #2 выполнил(а):
- Касьянов Никита Андреевич
- ХИ41
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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
  - Просмотрев видеоматериалы, я начал повторять последовательность приведённых действий
    - Создал новый 3D-проект [[1]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/1.jpg)
    - Ознакомился с сайтом заготовленных ассетов "Unity Asset Store" и, с его помощью, добавил в свой проект модели драконов и огненные эффекты. [[2]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/2.jpg) [[3]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/3.jpg)
    
    - C помощью драконов, сфер и плоскостей создал сцену, аналогичную сцене из обучающего видео, видоизменив оттенки. Также, создал DragonEgg, Energy Shield и несколько новых материалов. [[4]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/4.jpg)
    - Добавил анимационный контроллер дракону, попросив его летать в пространстве при старте сцены.  [[5]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/5.jpg) [[6]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/6.jpg)
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

    - Далее, добавил скрипт падения яиц с некоторой переодичностью, так же, используя видеоматериалы
    ```c#
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

    ```
    - Затем, добавил эффекты, припадениии яиц о текстуру плоскости и добавил скрипт исчезновения яиц при столкновении с плоскостью [[7]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/7.jpg)
    ```c#
     public class DragonEgg : MonoBehaviour
    {
    public static float bottomY = -30f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    private void OnTriggerEnter(Collider other) {
        ParticleSystem ps = GetComponent<ParticleSystem>();
        var em = ps.emission;
        em.enabled = true;

        Renderer rend;
        rend = GetComponent<Renderer>();
        rend.enabled = false;
    }
    void Update()
    {
        if (transform.position.y < bottomY){
            Destroy(this.gameObject);
        }
    }

    ```
    - Так же, был создан основной скрипт игры, который прикреплён к камере, и в нем были записаны строки появления 3-х энергитических щитов при старте сцены
          ```c#
                 public class DragonPicker : MonoBehaviour
              {
                  public GameObject energyShieldPrefab;
                  public int numEnergyShield = 3;
                  public float energyShieldBottomY = -6f;
                  public float energyShieldRadius = 1.5f;

                  // Start is called before the first frame update
                  void Start()
                  {
                      for(int i = 1; i <=  numEnergyShield; i++){
                          GameObject tShieldGo = Instantiate<GameObject>(energyShieldPrefab);
                          tShieldGo.transform.position = new Vector3(0, energyShieldBottomY, 0);
                          tShieldGo.transform.localScale = new Vector3(4*i,1*i,4*i);
                      }
                  }

                  // Update is called once per frame
                  void Update()
                  {

                  }
              }

          ```
    - В итоге, получилась такая незамысловатая но интересная сцена [[8]](https://github.com/Kasyanov-git/DA-in-GameDev-lab2/blob/main/8.jpg)
    
## Задание 2
### В проект, выполненный в предыдущем задании, добавить систему проверки того, что SDK подключен (доступен в режиме онлайн и отвечает на запросы);
  - Ход работы.
    - В оффициальной документации, во вкладке Установка и использование SDK, нашел как установить и использовать SDK в своём проекте. [[2.1]]()
    - Для того, чтобы использовать предложенные HTML строки, в Unity, во вкладке File, перешёл в меню Build Settings.
В поле Scences in build перетащил рабочую сцену проекта, после выбрал WebGl платформу, необходимую для портала Яндекс Игры. [[2.2]]()
    - Затем проект был собран в папку. При сборке, появилля основной INDEX.html файл, открыв который, в редакторе кода, мы вставили необходимые кусочки подключения и проверки Яндекс SDK:
```HTML

  <!-- Yandex Games SDK -->
  <script src="https://yandex.ru/games/sdk/v2"></script>

```
а так же:
```HTML

   YaGames
      .init()
      .then(ysdk => {
          console.log('Yandex SDK initialized');
          window.ysdk = ysdk;
    });

```
   - Сохранив изменения, в Unity, вместо Build нажал Build and Run, и после сборки и компиляции проекта, тот был развёрнут на локальном сервере и работал обособленно от Unity. 
   - Открыв Консоль Браузера, я увидел сообщение, что Яндекс SDK был инициализирован, а значит всё правильно сработало. [[2.3]]()


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
