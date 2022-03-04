# hse_hw2_chip

ChIP-seq данные: 
- Клеточная линия: MCF-7
- Реплики: ENCFF522RPS и ENCFF428DVP
- Контроль: ENCFF640MKX

Ссылка на Google Colab:
https://colab.research.google.com/drive/1w9OCQjMJw_mB0d017SV5IFVekuJWWgwm?usp=sharing

### Анализ отчетов FastQC по трем образцам:

- Summary

     ENCFF522RPS | ENCFF428DVP | ENCFF640MKX 
     --- | --- | --- 
     ![image](https://user-images.githubusercontent.com/60548614/156811837-30444cdf-a031-4974-bfac-0f605b7805b5.png) | ![image](https://user-images.githubusercontent.com/60548614/156812494-59b2131a-865c-4f55-adf7-7443b321ec91.png) | ![image](https://user-images.githubusercontent.com/60548614/156811977-2b809fa6-0635-407b-9261-12347efefab7.png)
 
Вмдно, что большинство анализов проведены корректно, однако в образце ENCFF428DVP чрезмерно встречается определенная последовательность![image](https://user-images.githubusercontent.com/60548614/156812372-55dc8fe5-44f9-4bab-9e1e-151e8afd9813.png)
 
Несмотря на это, по параметру Per tile sequence quality видно, что этот образец идеален. Незначительные потери в качестве наблюдаются как раз в реплике ENCFF522RPS и контроле (более светлые полосы). Однако все значения в пределах нормы, поэтому в фильтрации или подрезание чтений нет необходимости.

- Per tile sequence quality

     ENCFF522RPS | ENCFF428DVP | ENCFF640MKX 
     --- | --- | --- 
    ![image](https://user-images.githubusercontent.com/60548614/156816084-3b6ca067-a835-4b3a-9e62-fa057a4aa2a7.png) | ![image](https://user-images.githubusercontent.com/60548614/156816120-a326508b-b8c5-44d3-b4a0-8d803a306760.png) | ![image](https://user-images.githubusercontent.com/60548614/156816155-a41a0313-bef6-4d7c-b8a7-ad5a0aa58ab8.png)
 
Остальные параметры:
- Basic statistics
     ENCFF522RPS | ENCFF428DVP | ENCFF640MKX
     --- | --- | --- 
     ![image](https://user-images.githubusercontent.com/60548614/156814826-db836bf3-a3ed-4f65-987b-77c25edd8ed5.png) | ![image](https://user-images.githubusercontent.com/60548614/156814866-15bd7679-99f3-4bbe-b3e3-0b3c4e7ae78e.png) | ![image](https://user-images.githubusercontent.com/60548614/156814901-5c4d15fd-1246-4456-9400-e047203b45ee.png)
      
- Per base sequence content
     ENCFF522RPS | ENCFF428DVP | ENCFF640MKX 
     --- | --- | --- 
     ![image](https://user-images.githubusercontent.com/60548614/156815904-3f7aa2aa-d6b9-4a4a-8ebe-b3be3aa5b997.png) | ![image](https://user-images.githubusercontent.com/60548614/156815956-936280be-2041-4375-bff3-dbc7187ad4e1.png) | ![image](https://user-images.githubusercontent.com/60548614/156816016-964fb369-031c-4fe6-b2da-2c4f8c889ad4.png)
Видно, что содержания азотистых оснований у реплик слегка колеблятся на всех позициях, но, я думаю, это не критично. Причем у контроля небольшое колебание процентов задетектировано только в начале ридов.
     
- Per sequence GC content
     ENCFF522RPS | ENCFF428DVP | ENCFF640MKX 
     --- | --- | --- 
     ![image](https://user-images.githubusercontent.com/60548614/156816466-85957f8e-e1c7-4caf-bc55-4dc3ef7b6240.png) | ![image](https://user-images.githubusercontent.com/60548614/156816502-586b0733-00b5-4dfe-9310-787dea617732.png) | ![image](https://user-images.githubusercontent.com/60548614/156816549-f8f6c606-abd3-415a-8979-abb037a0fa4b.png)
      
Графики имеют вид нормального распределения, однако не совсем точно соотносятся с теоретическим. Однако эти выборсы не критичны.

### Таблица с результатами выравнивания по каждому из 3 образцов

![image](https://user-images.githubusercontent.com/60548614/156818085-8ade162b-2e4d-4439-a018-c1351f24c0b6.png)

Процент выравнивания очень низкий - даже меньше, чем неспецифичный контроль - потому что, во-первых, скорее всего малая доля модификаций гистонов типа H3K4me1 выпадает на 14-ую хромосому, а во-вторых, сама хромосома достаточно короткая.
  
### Диаграммы Венна
   
- ENCFF522RPS
     Сколько пиков из ENCFF522RPS пересекается с ENCFF583NFB  |  Сколько из ENCFF583NFB пересекается с ENCFF522RPS
     --- | --- 
     ![image](https://user-images.githubusercontent.com/60548614/156818610-c50d15a0-a699-4cca-99d6-befd08df44b8.png) | ![image](https://user-images.githubusercontent.com/60548614/156818648-6b1fb768-f7d3-4f49-b80a-28a9a3b4a88d.png)
     
 - ENCFF428DVP
     Сколько пиков из ENCFF428DVP пересекается с ENCFF583NFB  |  Сколько из ENCFF583NFB пересекается с ENCFF428DVP
     --- | --- 
     ![image](https://user-images.githubusercontent.com/60548614/156819223-548c382c-ea53-4353-84c0-d6976f88d916.png) | ![image](https://user-images.githubusercontent.com/60548614/156819246-ef408c56-1780-4712-b757-7bd9bd7a8e3d.png)

Видно, что количество пересекающихся учатсков относительно небольшое. Скорее всего это произошло из-за того, что изначально мы производили выравнивание на одну хромосому, поэтому само количество пиков у реплик небольшое. В файле ENCFF583NFB, взятом из ENCODE, количество пиков гораздо больше, так как он получен в результате выравнивания на все хромосомы.
