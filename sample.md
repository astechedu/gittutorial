$\mathcal{\color{purple}{this \ is \ a \ paragraph} \ \color{cyan}{in \ another \ font}}$

$\mathbb{\color{teal}{this \ is \ a } \ \color{magenta}{paragraph \ in \ another \ font}}$

$\mathscr{\color{red}{this} \ \ \color{blue}{is \ \ a \ \ paragraph} \ \ \color{yellow}{in \ \ another \ \ font}}$

$\mathfrak{\color{lime}{this \ is \ a \ paragraph \ in \ another \ font}}$

$\mathscr{\color{red}{mon}\color{white}{day}}$

$\textcolor{olive}{\TeX} \ \textcolor{darkgray}{workaround \ found \ by \ Dassalem \ Mohammed \ Yasser}$

$\textit{hello}$  #italic

$\text{hello}$    #normal

$\Large{hello}$$   #Bigger text size

$$\LaTeX$$






Color Marking :

$\colorbox{red}{text}$

Text inside bordered Box 

$\fbox{Hello there}$




$\color[rgb]{1,0,1} hello$

$\color[RGB]{155,127,0} hello$

$\color[gray]{0.3} hello$





This is a workaround to change text font , color and also size in GFM using MathJaX

this is a preview for how it looks like:

enter image description here possible fonts :

    mathcal - mathbb - mathscr - mathfrak - mathcal

possible colors :

    black, blue, brown, cyan, darkgray, gray, green, lightgray, lime, magenta, olive, orange, pink, purple, red, teal, violet, white, yellow

    use $..$ for inline code and $$..$$ for centered
    u can use \color or \textcolor
    u can use \ between text as a space (or \ \ for double space)




U can go advanced with coloring text : possible models : gray - rgb - RGB
Model 	Desc 	values
gray 	Shades of gray 	0.1 to 1.0
rgb 	red,green,blue 	[0-255]{3}
RGB 	Red,Green,Blue 	[0-255]{3}




To do this just add tags such as these samples to your README.md file:

```json
   // code for coloring
```
```html
   // code for coloring
```
```js
   // code for coloring
```
```css
   // code for coloring
```
// etc.

No "pre" or "code" tags needed.