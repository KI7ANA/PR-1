<div align="center">

# Отчет

</div>

<div align="center">

## Практическая работа №1

</div>

<div align="center">

## Практическая работа №1 Знакомство с Android Studio

</div>

**Выполнил:**  
Ткачев Сергей Юрьевич  
**Курс:** 2  
**Группа:** ИНС-б-о-24-2  
**Направление:** ИПИНЖ (Институт перспективной инженерии) 
**Профиль:** Информационные системы и технологии  

---

### Цель работы

Изучение интерфейса Android studio и создание первого простого приложения.

### Ход работы
## 1. В начале работы Android Studio был скачен, установлен и настроен согласно методичке. Создан и запущен новый проект "PW_1".

<div align="center">

<img width="1909" height="1022" alt="image" src="https://github.com/user-attachments/assets/14cc53e0-10ee-4cf1-8e55-fe9438841932" />

</div>

<div align="center">

## 2. В имени приложения, путём изменения содержимого файла "strings.xml", было указано авторство.

<img width="738" height="162" alt="image" src="https://github.com/user-attachments/assets/e177cb9b-6c9c-48fc-869d-1b2dc5866e8f" />

</div>

## 3. На странице приложения указана дата рождения с помощью свойства страницы TextView.

<div align="center">

<img width="1909" height="1022" alt="image" src="https://github.com/user-attachments/assets/14cc53e0-10ee-4cf1-8e55-fe9438841932" />

## 4. Выполнениы все описанные в работе шаги. В частности отрисованы: прямоугольник, круг, отрезок и кривые с разным углом наклона. Координаты отрезка и кривых были изменены так, чтобы фигуры не лежали друг на друге. Выполнено задание согласно варианту: отрисован красный овал, с длиной вертикальной полуоси в 3 раза большей горизонтальной.

<div align="center">

<img width="1905" height="964" alt="image" src="https://github.com/user-attachments/assets/76745c14-ef85-4a83-a498-6da150cbf362" />

## Листинг 1. - класс DrawView для задания 3

@Override
protected void onDraw(Canvas canvas) {
    canvas.drawARGB(255, 230, 230, 250);

    p.setStyle(Paint.Style.FILL);
    p.setColor(Color.MAGENTA);

    int side = 160; // увеличили для наглядности
    int left = 200;
    int top = 250;
    int right = left + side;
    int bottom = top + side;

    canvas.drawRect(left, top, right, bottom, p);
}
  
<img width="503" height="815" alt="image" src="https://github.com/user-attachments/assets/08c8e44c-5822-4a4f-89dd-324618bfecef" />

</div>

## 5. Выполнено задание 4 согласно варианту: пурпурный квадрат, площадь которого в 2 раза больше периметра.

## Листинг 2. - class DrawView для задания 4

package com.ncfu.pw_1;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.os.Bundle;
import android.view.View;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setTitle("PW_1 Сергей");
        setContentView(new DrawView(this));
    }

    class DrawView extends View {
        Paint p;

        public DrawView(Context context) {
            super(context);
            p = new Paint();
            p.setAntiAlias(true);
        }

        @Override
        protected void onDraw(Canvas canvas) {
            super.onDraw(canvas);

            int w = getWidth();
            int h = getHeight();

            Paint sky = new Paint();
            Paint ground = new Paint();
            Paint sun = new Paint();
            Paint rail = new Paint();
            Paint sleepers = new Paint();
            Paint horizon = new Paint();
            Paint linePaint = new Paint();

            sky.setColor(Color.rgb(180, 220, 255));
            ground.setColor(Color.rgb(170, 210, 140));
            sun.setColor(Color.YELLOW);
            rail.setColor(Color.DKGRAY);
            sleepers.setColor(Color.rgb(139, 69, 19));
            horizon.setColor(Color.rgb(90, 140, 90));
            linePaint.setColor(Color.BLACK);

            rail.setStrokeWidth(8);
            sleepers.setStrokeWidth(10);
            horizon.setStrokeWidth(4);
            linePaint.setStrokeWidth(4);

            // Небо
            canvas.drawRect(0, 0, w, h / 2, sky);

            // Земля
            canvas.drawRect(0, h / 2, w, h, ground);

            // Солнце
            canvas.drawCircle(w - 120, 120, 50, sun);

            // Горизонт
            canvas.drawLine(0, h / 2, w, h / 2, horizon);

            // Рельсы
            int bottomY = h;
            int horizonY = h / 2 + 40;

            int leftRailBottomX = w / 2 - 180;
            int rightRailBottomX = w / 2 + 180;

            int leftRailTopX = w / 2 - 25;
            int rightRailTopX = w / 2 + 25;

            // Внешние линии рельс
            canvas.drawLine(leftRailBottomX, bottomY, leftRailTopX, horizonY, rail);
            canvas.drawLine(rightRailBottomX, bottomY, rightRailTopX, horizonY, rail);

            // Внутренние линии рельс
            canvas.drawLine(leftRailBottomX + 20, bottomY, leftRailTopX + 8, horizonY, rail);
            canvas.drawLine(rightRailBottomX - 20, bottomY, rightRailTopX - 8, horizonY, rail);

            // Шпалы
            for (int i = 0; i < 9; i++) {
                float k = i / 8.0f;

                int y = (int) (bottomY - k * (bottomY - horizonY));
                int halfWidth = (int) (170 - k * 145);

                canvas.drawLine(w / 2 - halfWidth, y, w / 2 + halfWidth, y, sleepers);
            }

            // Ломаная слева для выполнения условия задания
            float[] polyline = {
                    40, h / 2 + 120,
                    80, h / 2 + 80,
                    120, h / 2 + 100,
                    170, h / 2 + 60,
                    220, h / 2 + 90
            };
            canvas.drawLines(polyline, linePaint);
        }
    }
}

<img width="1203" height="912" alt="image" src="https://github.com/user-attachments/assets/b6bf8a40-a307-43a5-bfac-86f6dfd6adcf" />

</div>

*Примечание по вставке изображений:*
*Скриншоты необходимо предварительно загрузить в репозиторий (например, в папку `images/`). Ссылка должна вести на файл внутри репозитория, а не на локальный диск вашего компьютера.*

### Вывод
В результате выполнения практической работы я [краткий вывод: что изучил, чему научился, что разработал].

### Ответы на контрольные вопросы
1.  **Вопрос 1:** [Ваш развернутый ответ на первый вопрос из методички].
2.  **Вопрос 2:** [Ваш ответ на второй вопрос].
3.  **Вопрос 3:** [Ваш ответ на третий вопрос].

