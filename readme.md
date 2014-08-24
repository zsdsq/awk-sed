The Awk text-processing programming language and is a useful tool for manipulating text

recognize file -> record(line) -> field
$n from 1 to ... fields, $0 - record

gawk '{ sum += $1 }; END { print sum }' file
gawk -F: '{ print $1 }' /etc/passwd

Some of the commonly used built-in variables are:

    NR -- The current line's sequential number
    NF -- The number of fields in the current line
    FS -- The input field separator; defaults to whitespace and is reset by the -F command line parameter 

awk 'BEGIN{print"fee"} $1=="foo"{print"fi"}
     END{print"fo fum"}' filename

BEGIN AND END block 1 times exec

/// array and script
console: awk -f test1 readme.md

test1:
#!/usr/bin/awk -f
{for(i=1;i <=NF;i++) freq[$i]++ }
END{for(word in freq) print word, freq[word]
}



/// reg exp

cat abc.txt|awk '/[0-9]+.[0-9]*/ { print }'

/// expr

$1 == "fred" { print $3 }

$5 ~ /root/ { print $3 } 

/// все где встречается root

awk '{
   if ( $1 ~ /root/ )
  {
   print $1
  }
}' /etc/passwd

///

( $1 == "foo" ) && ( $2 == "bar" ) { print } 

.......................................................


Печать каждой строки стрирая перед этим поле 2

awk '{$2 = ""; print}' file

Напеччатать hi 48 раз

yes | head -48 | awk '{ print "hi" }'

РАспечатать от hi.0010 до hi.0099

yes | head -90 | awk '{printf("hi.00%2.0f\n", NR+9)}'

распечатать если поле $3 < 1900 (в myfile.txt). Если данные в поле 3 не числовые строка пропускается без вывода ошибок

cat myfile.txt| awk '{if ($3 < 1900) print $3, " ",$5,$7,$8}'

Подсчитать число строк в которых 3-е поле > 1-го

awk '$3 > $1 {print i + "1"; i++}' file

распечать строки в которых меньше 65 символов

awk 'length < 64'

SED

Синтакс регэкспов такой же как и grep, но / здесь спец символ

///
/// замена выражений
///

общий вид:

s/regular-expression/replacement text/{flags}

пример

sed -e 's/black/white/g' file

-e опция: дальше идет выражение, вместо этого можно было написать sed -f scriptfile file

s - найти и заменить, g - флаг, заменить во всех совпадениях

/ @ % , ; : - в качестве разделителя можно использовать любой символ главное чтобы их было 3

например:
sed -e 's@/usr/bin@usr/etc@' file

иначе при исп / пришлось бы писать 
sed -e 's/\/usr\/bin/\/usr/etc/' file

/// подстановка прочтенных символов

& позволяет использовать заменяемые символы в замене.
Например менять 99 на (99) или даже 99 на 9999, не уточняя что мы имеем дело только с 9
echo "99 asd99" | sed 's/[0-9][0-9]*/&&/' выведет 9999 asd99

по умолчанию sed не знает знака +, для включения доп символов рег выр-й есть флаг -r
echo "99 asd99" | sed -r 's/[0-9]+/&&/'

/// 






