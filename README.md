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
### Первые чтения
