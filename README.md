# Typewritter-HTML-CSS-ONLY

Small project to learn how to create a typewritter effect using only HTML and CSS. <br>
Step by step 🐌

## Step 1 : Tree structure


```
~Typewritter-HTML-CSS-ONLY
                |__index.html
                |__style.css
```

Create our index.html with boiler plate and a css file

<hr>

## Step 2 : HTML

In your body, add a container and a child which will be your content

```
<body>
    <div class="container">
        <h1 class="content">
        Start of your sentence
            <ol>
                <li><span>Sentence 1</span></li>
                <li><span>Sentence 2</span></li>
                <li><span>Sentence 3</span></li>
                <li><span>Sentence 4</span></li>
            </ol>
        </h1>
    </div>
</body>
```

🚩RED FLAG : How many \<li> you use, will be meaningfull

<hr>

## Step 3 : CSS

Let's make it pretty before animation
In your css file

### Step 3.1 : Reset

```
/* ALWAYS, reset : */
*{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    /* Change your font if you want to */
    color: #ffffff;
}
```

### Step 3.2 : Style your container of your container (here \<body>)

```
body{
    height: 100vh;
    width: 100vw;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #242424;
}
```

### Step 3.3 : Position for container

```
.container{
    position: absolute;
    top: 20%;
    padding: 5%;
}
```

### Step 3.4 : Ordered List 

```
.container .content ol{
    /* Remove 1. 2. 3. ... */
    list-style: none;

    /* This way, only ONE sentence will take 100% height of the content container */
    --height: 2em;
    height: var(--height);
    line-height: var(--height);

    /* Hide other sentences that are out of the content container*/
    /* Comment overflow line if you want to see how it works*/
    overflow: hidden; 
}
```

### Step 3.5 : Make your text pretty

```
/* This is our sentences/words */
.container .content ol li span{
    font-weight: 600;
    /* Make your take transparent */
    color: transparent;
    /* Background of your sentence/word gradient */
    background: linear-gradient(to right, #2593ee, #bee62d);
    /* This way your text will take your gradient as its color */
    background-clip: text;
}
```
<hr>

## Step 4 : Animation

### Step 4.0.5 : animation slide-up (optionnal)

```
/* ADD your animation to your li's */
.container .content ol li{
    animation: slide-up 12s infinite;
}

@keyframes slide-up {
    0%, 10%{
        transform: translateY(0%);
    }
    15%, 25%{
        transform: translateY(-100%);
    }
    30%, 40%{
        transform: translateY(-200%);
    }
    45%, 55%{
        transform: translateY(-300%);
    }
}
```

### Step 4.1 : First animation cursor (blinking animation)

```

.container .content ol li span{

    [...]

    /* This will mimic a typewritter cursor */
    border-right: 3px solid #fff;
    animation: cursor .8s step-end infinite;

}

@keyframes cursor {
    /* Since it's already white, you only to make it disapear */
    50%{
        border-color: transparent;
    }
}
```

### Step 4.2 : Second animation typing

This one needs a lot of changes 

```
.container .content ol{

    [...]    

    display: flex;
    flex-flow: column nowrap;
    justify-content: flex-start;
    align-items: flex-start;
}

.container .content ol li span{

    [...]

    white-space: nowrap;

    display: inline-block;

    animation: 
    cursor .6s step-end infinite,
    typing 2s steps(9) infinite alternate;
}

@keyframes typing {
    0%,10%{
        width: 0%;
    }
    70%,100%{
        /* 103% for a gap */
        width: 103%;
    }
}
```

### Step 4.3 : Third and Last animation "slide" (the one that matters the most)

```

.container .content ol li{
    /* calc(nbr of steps * time of typing animation * 2 since it's an alternate) */
    animation: slide calc(4*2*2s) steps(4) infinite;
}

@keyframes slide {
    100%{
        transform: translateY(-400%);
    }
}

```