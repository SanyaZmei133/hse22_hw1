# hse22_hw1
Седых Александр Группа 2    
# Основное задание:
## Команды
### 1. Создаём ярлыки для файлов
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
### 2. Выбираем случайные чтения cbl 827
    seqtk sample -s827 oil_R1.fastq 5000000 > sub1.fastq
    seqtk sample -s827 oil_R2.fastq 5000000 > sub2.fastq
    seqtk sample -s827 oilMP_S4_L001_R1_001.fastq 1500000 > mp1.fastq
    seqtk sample -s827 oilMP_S4_L001_R2_001.fastq 1500000 > mp2.fastq
### 3. Используем программы fastqc и multiqc
    mkdir fastqc
    ls sub* mp* | xargs -tI{} fastqc -o fastqc {}
    mkdir multiqc
    multiqc -o multiqc fastqc
### 4. Подрезанием чтения
    platanus_trim sub*
    platanus_internal_trim mp*
### 5. Удаление изначальных файлов
    rm sub1.fastq 
    rm sub2.fastq
    rm mp1.fastq
    rm mp2.fastq
### 6. Используем программы fastqc и multiqc для подрезанных файлов
    mkdir fastqc_trimmed
    ls sub* mp*| xargs -tI{} fastqc -o fastqc_trimmed {}
    mkdir multiqc_trimmed
    multiqc -o multiqc_trimmed fastqc_trimmed
### 7. Сбор контигов, используя platanus assemble
    time platanus assemble -o Poil -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log
### 8. Сбор скаффолдов, используя platanus scaffold
    time platanus scaffold -o Poil -c Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 mp1.fastq.int_trimmed mp2.fastq.int_trimmed 2> scaffold.log
### 9. Уменьшение числа гэпов, используя platanus gap_close
    time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 mp1.fastq.int_trimmed mp2.fastq.int_trimmed 2> gapclose.log
### 10. Удаление подрезанных чтений
    rm sub1.fastq.trimmed
    rm sub2.fastq.trimmed
    rm mp1.fastq.int_trimmed
    rm mp2.fastq.int_trimmed
***
## Статистика и результаты отчёта
### Первые чтения:
![Скриншот 1](Screenshot_1.png)
![Скриншот 2](Screenshot_2.png)
![Скриншот 3](Screenshot_3.png)
![Скриншот 4](Screenshot_4.png)
![Скриншот 5](Screenshot_5.png)
![Скриншот 6](Screenshot_6.png)
![Скриншот 7](Screenshot_7.png)
![Скриншот 8](Screenshot_8.png)
![Скриншот 9](Screenshot_9.png)
![Скриншот 10](Screenshot_10.png)
***
### После подрезания чтений:
![Скриншот 11](Screenshot_11.png)
![Скриншот 12](Screenshot_12.png)
![Скриншот 13](Screenshot_13.png)
![Скриншот 14](Screenshot_14.png)
![Скриншот 15](Screenshot_15.png)
![Скриншот 16](Screenshot_16.png)
![Скриншот 17](Screenshot_17.png)
![Скриншот 18](Screenshot_18.png)
![Скриншот 19](Screenshot_19.png)
![Скриншот 20](Screenshot_20.png)
![Скриншот 21](Screenshot_21.png)
***
## Код анализа данных
[Код анализа данных в google colab](https://colab.research.google.com/drive/1Dgivk-jPKynshjqji1PME2uCT1UTFxvc?usp=sharing)
***
## Вывод
1. Мало конгитов - 190
2. N50 скафолда 1035602, поолное покртыие длины
3. Общая длина - 1035602
***
# Бонусная часть:
***
### Уменьшили количество чтений с 5 миллионов и 1,5 миллиона до 1 и 0,5 миллионов соответственно
    seqtk sample -s827 oil_R1.fastq 1000000 > sub1.fastq
    seqtk sample -s827 oil_R2.fastq 1000000 > sub2.fastq
    seqtk sample -s827 oilMP_S4_L001_R1_001.fastq 500000 > mp1.fastq
    seqtk sample -s827 oilMP_S4_L001_R2_001.fastq 500000 > mp2.fastq
***
## Статистика и отчёт
### Первые чтения:
![Скриншот 22](screenshots/Screenshot_22.png)
![Скриншот 23](screenshots/Screenshot_23.png)
![Скриншот 24](screenshots/Screenshot_24.png)
![Скриншот 25](screenshots/Screenshot_25.png)
![Скриншот 26](screenshots/Screenshot_26.png)
![Скриншот 27]screenshots/(Screenshot_27.png)
![Скриншот 28](screenshots/Screenshot_28.png)
![Скриншот 29](screenshots/Screenshot_29.png)
![Скриншот 30](screenshots/Screenshot_30.png)
![Скриншот 31](screenshots/Screenshot_31.png)
***
### После подрезания чтений:
![Скриншот 32](screenshots/Screenshot_32.png)
![Скриншот 33](screenshots/Screenshot_33.png)
![Скриншот 34](screenshots/Screenshot_34.png)
![Скриншот 35](screenshots/Screenshot_35.png)
![Скриншот 36](screenshots/Screenshot_36.png)
![Скриншот 37](screenshots/Screenshot_37.png)
![Скриншот 38](screenshots/Screenshot_38.png)
![Скриншот 39](screenshots/Screenshot_39.png)
![Скриншот 40](screenshots/Screenshot_40.png)
![Скриншот 41](screenshots/Screenshot_41.png)
![Скриншот 42](screenshots/Screenshot_42.png)
***
## Код анализа данных
[Код анализа данных в google colab](https://colab.research.google.com/drive/1HKFa8hzziD92CKbInv8ALWJMkq8sDpFK?usp=sharing)
***
## Вывод
1. Много конгитов - 1277
2. N50 скафолда 1890955, примерно 50% покрыто
3. Общая длина - 3853384
***
# Сравнение
После уменьшения количества чтений качетво сборки упало, стало больше контигов, увеличилась общая длина, но многие параметры отчёта остались на приверно тех же уровнях, поэтому можно сказать, что общее качество не сильно ухудшилось.
