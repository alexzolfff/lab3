<p align="center">МИНИСТЕРСТВО НАУКИ  И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ  <br/>
Федеральное государственное автономное образовательное учреждение высшего образования  <br/>
"КРЫМСКИЙ ФЕДЕРАЛЬНЫЙ УНИВЕРСИТЕТ им. В. И. ВЕРНАДСКОГО"  <br/>
ФИЗИКО-ТЕХНИЧЕСКИЙ ИНСТИТУТ  <br/>
Кафедра компьютерной инженерии и моделирования<br/></p>
<br/>

### <p align="center">Отчёт по лабораторной работе № 3<br/> по дисциплине "Программирование"</p>
<br/>
​Cтудента 1 курса группы ПИ-б-о-192(2)<br/>
Золотого Александра Витальевича<br/>
направления подготовки 09.03.04 "Программная инженерия"  
<br/>
<br/>

<table>
<tr><td>Научный руководитель<br/> старший преподаватель кафедры<br/> компьютерной инженерии и моделирования</td>
<td>(оценка)</td>
<td>Чабанов В.В.</td>
</tr>
</table>
<br/><br/>

<p align="center">Симферополь, 2020</p>


### Тема: Дешифровка текста из изображения.
**Цель:**
1.Закрепить навыки разработки программ использующих операторы цикла;
2.Закрепить навыки разработки программ использующих массивы;
3.Освоить методы подключения сторонних библиотек.


**<p align="center">Ход работы:</p>**

Код программы:
```cpp
#include <iostream>
#include "libbmp.h"

using namespace std;

bool getCharR(BmpImg* img, int x, int y, int& count, int& toByte) {
	toByte = toByte + (img->red_at(x, y) % 2) * pow(2, count);
	return true;
}

bool getCharG(BmpImg* img, int x, int y, int& count, int& toByte) {
	toByte = toByte + (img->green_at(x, y) % 2) * pow(2, count);
	return true;
}

bool getCharB(BmpImg* img, int x, int y, int& count, int& toByte) {
	toByte = toByte + (img->blue_at(x, y) % 2) * pow(2, count);
	return true;
}

bool check(int& count, int& toByte) {

	if (count == 0)
	{
		if (char(toByte) == '\0') return false;

		std::cout << char(toByte);

		count = 8;
		toByte = 0;
	}
	return true;
}

int main()
{
	BmpImg img;
	img.read("pic4.bmp");
	int count = 7;
	int toByte = 0;

	for (int i = img.get_width() - 1; i >= 0; i--)         // KEY   11r 11g 11b 10r 10g 10b 01r 01g
		for (int j = img.get_height() - 1; j >= 0; j--)
		{
			if (!(getCharR(&img, i, j, count, toByte)&& check(count, toByte))) return 0;
			count--;

			if (!(getCharG(&img, i, j, count, toByte) && check(count, toByte))) return 0;
			count--;

			if (!(getCharB(&img, i, j, count, toByte) && check(count, toByte))) return 0;
			count--;
		}
}
```
Исходное изображение:

![](img/pic4.bmp)

><center>Рисунок 1. Заданное изображение
	
	
Декодированный текст:

James Madison Jr. (March 16, 1751[b] Ц June 28, 1836) was an American statesman, lawyer, diplomat, philosopher and Founding Father who served as the fourth president of the United States from 1809 to 1817. He is hailed as the "Father of the Constitution" for his pivotal role in drafting and promoting the Constitution of the United States and the United States Bill of Rights. He co-wrote The Federalist Papers, co-founded the Democratic-Republican Party, and served as the fifth United States secretary of State from 1801 to 1809.
Born into a prominent Virginia planter family, Madison served as a member of the Virginia House of Delegates and the Continental Congress during and after the American Revolutionary War. He became dissatisfied with the weak national government established by the Articles of Confederation and helped organize the Constitutional Convention, which produced a new constitution to supplant the Articles of Confederation. Madison's Virginia Plan served as the basis for the Constitutional Convention's deliberations, and he was one of the most influential individuals at the convention. Madison became one of the leaders in the movement to ratify the Constitution, and he joined with Alexander Hamilton and John Jay in writing The Federalist Papers, a series of pro-ratification essays that is widely considered to be one of the most influential works of political science in American history.
After the ratification of the Constitution, Madison emerged as an important leader in the United States House of Representatives and served as a close adviser to President George Washington. He was the main force behind the ratification of the United States Bill of Rights, which enshrines guarantees of personal freedoms and rights within the Constitution. During the early 1790s, Madison came to oppose the economic program and accompanying centralization of power favored by Secretary of the Treasury Alexander Hamilton. Along with Thomas Jefferson, Madison organized the Democratic-Republican Party, which was, alongside Hamilton's Federalist Party, one of the nation's first major political parties. After Jefferson won the 1800 presidential election, Madison served as secretary of State from 1801 to 1809. In that position, he supervised the Louisiana Purchase, which doubled the size of the United States.
Madison succeeded Jefferson with a victory in the 1808 presidential election. After diplomatic protests and a trade embargo failed to end British attacks against American shipping, he led the United States into the War of 1812. The war was an administrative morass and ended inconclusively, but many Americans saw it as a successful "second war of independence" against Britain. The war convinced Madison of the necessity of a stronger federal government, and he presided over the creation of the Second Bank of the United States and the enactment of the protective Tariff of 1816. He retired from public office in 1817 and died in 1836. Madison is considered to be one of the most important Founding Fathers of the United States, and historians have generally ranked him as an above-average president.

**Вывод:**
В ходе лабораторной работы я закрепил навыки разработки программ использующих операторы цикла и использующих массивы; освоил методы подключения сторонних библиотек.
