# **Regular expressions (Regex)**

![xkcd](https://homerhanumat.github.io/r-notes/images/xkcd-regex-save-day.png)

One the biggest problems that we have is keeping our data is certain order, either taking field notes or in the lab. :honeybee: :bookmark_tabs:
Additionally, sometimes our spreadsheets or annotations need to be reorganized according to new needs that arise when we are analyzing the data. We spend a lot of time doing this. Well, maybe this nightmare is going to be over, because today we'll see that these changes can be done in seconds using the beautiful **Regular expressions (Regex)**

tip: When you are copying and pasting too much is because you need some _Regex_

What do we need?

1. A system that supports Regex, it can be a text editor (I like [Atom](https://atom.io/)), R, python....
2. A text or spreadsheet to modify 
3. Keep in mind some special characters called *wildcards*

Wildcard: Special character that represent an specific variation of characters 

I will show the general syntax using a text editor. Then, we'll move to R

## How the search and replace bar work?
1. Open your text editor and type `crtl + f`. You will have a search and replace bar like this one:
![barra](https://raw.githubusercontent.com/fcsalgado/bioinformatics_urosario/master/images/barra.png)
Please activate the button `.*`

2. Using the search and replace bar transform the following scientific name `Gasteracantha cancriformis` to `G. cancriformis`. Pretty easy, right? 

3. Using the same method, transform these three scientific names 

```
 Gasteracantha cancriformis
 Macracantha arcuata
 Austracantha minax
```
This is when it starts to get tricky 

Imagine now scientific names such as `Ameiva ameiva`. Impossible!

4. Let's use our first wildcard: `\w`. This wildcard represents any number `(0-9)`, letter `(A-z)` or under score `(_)`. Explore how it works. 

5. This is not enough, we need to learn a couple of extra things. wildcards such as `\w` works really good with the `+` symbol. Let's add it to the end of the wildcard. cool, now we captured a whole word. So, if we want to capture the first letter plus the other letters, it would be like this `\w\w+`. We are almost there, we need to figure it out how the replace bar works.

6. To use the replace bar, we need to use the symbols `()` and `$`. The first one is going to capture text from the search bar, and the second one is going to let us use the terms of the search bar the way we want. It sounds weird, but let's try this:

<p>Search bar: (\w)(\w+) </p>
<p>Replace bar: $2$1 </p>

Awesome, we moved the first letter of both words. To tell Atom (or the text editor that you are using) that we just want the word that is at the begging of the line, we can use the a symbol `^` that represents _The begging of the line_. Please add this symbol to your search term, it will look like this `(^\w)(\w+)`. What this wildcard is saying is: "Capture a 1st term that is the first word at the begging of the line, and also capture a 2nd term that is the other letter of the word". 

<p>First term: (^\w) </p>
<p>Second term: (\w+) </p>

## First exercise

Using regular expressions, transform this: 
```
Gasteracantha cancriformis
Macracantha arcuata
Austracantha minax
Ameiva ameiva
``` 
into this: 
```
G. cancriformis
M. arcuata
A. minax
A. ameiva
```

<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>Search bar: `(^\w)(\w+)`</p>
        </p>Replace bar: `$1.`</p>
    </div>
</details>


## Second exercise

**Important**

The wildcard `\s` represents any type of space

Using regular expressions, transform this: 
```
Gasteracantha cancriformis
Macracantha arcuata
Austracantha minax
Ameiva ameiva
``` 
into this: 

```
Gasteracantha cancriformis G. cancriformis
Macracantha arcuata M. arcuata
Austracantha minax A. minax
```
<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>Search bar: `(^\w)(\w+)\s(\w+)`</p>
        </p>Replace bar: `$1$2 $3 $1. $3`</p>
    </div>
</details>

## Third exercise

To capture weird terms such as `,` or `(` or `[`, we use the backslash symbol, like this: `\,` 

Transform this quote:

`"What speak to the soul, escapes our measurements." (Alexander von humboldt)`

Into this quote:

`“our measurements speak to the soul” humboldt.`

<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>Search bar: `^(\")\w+(\s+\w+.+)\,\s+\w+\s+(\w+.+)\.\"\s+\((\w+\s+)+(\w+)\)`</p>
        </p>Replace bar: `$1$3$2$1 $5`</p>
    </div>
</details>

## Wildcards are all you need

[A list wildcards and Regex tips](http://practicalcomputing.org/files/PCfB_Appendices.pdf) from a book called **Practical computing for biologist** that is awesome and available in the library. You can also download it from [here](https://drive.google.com/file/d/0B65PEDolIc6oSjVpMTVtY05wVkU/view?usp=sharing) today :wink:


## Real life example 1

Imagine that you download a lot of sequences from the GenBank, as the ones in this [Fasta file](https://raw.githubusercontent.com/fcsalgado/bioinformatics_urosario/master/files/16s_Aranediae.fas), they usually have a lot words:

`>MG670140.1 Actinacantha globulata isolate AGLO1 16S ribosomal RNA gene, partial sequence; mitochondrial`

which make difficult to identify species that are problematic in our alignments or make the phylogenetic tree unreadable. 

For example `>Actinacantha_globulata MG670140.1 16S` looks so much better and has all the info that we need :bowtie:

transform the format of the 216 sequences in this Fasta file [Fasta file](https://raw.githubusercontent.com/fcsalgado/bioinformatics_urosario/master/files/16s_Aranediae.fas) using Regex

<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>Search bar: `(\w+\.\d+)\s+(\w+)\s+(\w+)+.+(16S)+.+`</p>
        </p>Replace bar: `$1_$3 $2 $4`</p>
    </div>
</details>

## Real life example 2

Transform this space sepated [file](https://raw.githubusercontent.com/fcsalgado/bioinformatics_urosario/master/files/exercise_file.txt) into a CSV

<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>Search bar: `[ ]`</p>
        </p>Replace bar: `,`</p>
    </div>
</details>

-------------------------------------------------------------------------------------------------------------------------

## Let's move to R, which is why we are here

There are two ways to work with RegEx in R:

[Regex in base R](http://uc-r.github.io/regex)

[Regex in the Tidyverse](https://stringr.tidyverse.org/articles/regular-expressions.html)

**vitally important fact**

R uses double back slash, instead of one, for wildcards:

```
  "(?xi)       # ignore whitespace (x) and ignore case (i)
  \\b          # assert a word-boundary
  (\\w)        # capture the first letter of the first word
  \\w*         # rest of the first word
  \\W+         # one or more non-word characters
  \\1          # repeat the letter captured previously
  \\w*         # rest of the second word
  "
```

Let's start:

## Real life exercise 1

Imagine that you have a file with XX number of species and you now need to make comparisons within the species in each genus. The problem is that you have just a column with full species name. Let's create one new column: 

1. Load the data

`data<-read_csv("file_regex_aves.csv")`

2. Check how it looks

`head(data)`

3. RegEx magic

for base R, we will use *gsub*
for Tidyverse, we will use *str_extract* couple with *regex*

*First solution*
`data$genus<-gsub(pattern="(\\w+)\\s+\\w+",replacement="\\1",x=data$species)`
*more accurate solution*
`data$genus<-gsub(pattern="^(\\w+)\\s+\\w+$",replacement="\\1",x=data$species)`
*In the tidyverse*
`data$genus<-str_replace_all(pattern="(^\\w+)\\s+\\w+",replacement="\\1",string=data$species)`
or create two columns
`data %>% mutate(genus=str_replace_all(pattern="(^\\w+)\\s+\\w+",replacement="\\1",string=species),epithet=str_replace_all(pattern="^\\w+\\s+(\\w+)",replacement="\\1",string=species))`


## Real life exercise 2

Sometimes people ruin your life without even noticing, for example when they go to the field and share with you coordinates in the following format: 36°36'12''N

fortunately, Regex can fix you day really fast.

1. Load the data

`field_data<-read_csv("Marrus_claudanielis.txt")`

2. Check how it looks

`head(field_data)`

Really bad, right?

3. RegEx magic

Let's start replacing all the weird symbols **°** and **'** with some RegEx

`field_data$Lat<-field_data %>% pull(Lat) %>% str_replace_all(pattern="(\\°)|(\\'+)",replacement=" ")`
`field_data$Lon<-field_data %>% pull(Lon) %>% str_replace_all(pattern="(\\°)|(\\'+)",replacement=" ")`

Now let's use RegEx to split the string into three columns that we will use to transform our coodinates.....wait! 
Let's do it just for one string, and try our RegEx skills

string<-"122 22 48 W"

What do we need?


<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>`degrees<-str_replace_all(pattern="^(\\d+)\\s+.+",replacement="\\1",string=string) %>% as.numeric()`</p>
        </p>`minutes<-str_replace_all(pattern="^\\d+\\s(\\d+)+.+$",replacement="\\1",string=string) %>% as.numeric()`</p>
        </p>`seconds<-str_replace_all(pattern="^.+(\\d{2})\\s\\w+$",replacement="\\1",string=string) %>% as.numeric()`</p>
        </p>`new_coordinates<-degrees+((minutes+(seconds/60))/60)`</p>
    </div>
</details>

you can then try this for latitude and longitude. Ideally, you should find a way to transform them all at once. The best way is to create a function :)

## Real life exercise 3

The best way to solve future problems is to predict them. A nice way to start is to name the files that you'll create with some sort of sense. Let's imagine that you measured the heating rate of multiple eggs in multiple light treatments (UV,NIR,Full light) and named the files like this _Treatment_eggCode.CSV_. For your stats, you now need to create a 
dataFrame with four columns, one for the ID of the egg and three that contains how the temperature change (this correponds to the third column of each file) during the experiment in each treatment. 

What should we do? Probably use some RegEx to make this as simple as possible. 

1. How many eggs did you measure?

<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>`eggs<-dir() %>% gsub(pattern="\\w+\\_(\\w+).CSV",replacement="\\1") %>% unique()`)</p>
    </div>
</details>


2. What are the name of the treatments?

<details><summary><span style="font-size: 18pt;"><strong>Answer</strong></span></summary>
    <div>
        <p>`treat<-dir() %>% gsub(pattern="(\\w+)\\_\\w+.CSV",replacement="\\1") %>% unique()`</p>
    </div>
</details>

3. Now let's use a for loop to make our data frame


```
data_eggs<-NULL
for(g in eggs){
treat_temp<-tibble(egg=g)
for(t in treat){
    tmp<-read_csv(paste0(t,"_",g,".CSV"),col_names=FALSE)
    tmp<-tmp[,3]
    colnames(tmp)<-t
    delta_t<-tmp[nrow(tmp),t]-tmp[1,t]
    treat_temp<-cbind(treat_temp,delta_t)
}
data_eggs<-rbind(data_eggs,treat_temp)
}
```


































