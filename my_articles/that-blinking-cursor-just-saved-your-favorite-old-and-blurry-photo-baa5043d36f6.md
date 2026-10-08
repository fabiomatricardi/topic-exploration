---
post_id: "baa5043d36f6"
title: "That blinking cursor just saved your favorite old and blurry photo"
subtitle: "How a 30-year-old tech trick (the terminal) is the perfect partner for cutting-edge AI magic"
published: "2025-09-17T00:52:03.179Z"
url: "https://medium.com/@fabio.matricardi/that-blinking-cursor-just-saved-your-favorite-old-and-blurry-photo-baa5043d36f6"
earnings_usd: 6
---

# That blinking cursor just saved your favorite old and blurry photo

*How a 30-year-old tech trick (the terminal) is the perfect partner for cutting-edge AI magic*

---

![](../assets/1_95r85GEKSuxtEjxCR1NdWA.png)

*image by the author and Flux with this method*

You know that sinking feeling when you find the *perfect* photo — your dog mid-sneeze, your kid’s first pancake flip, that sunset that looked like a painting — but when you try to share it, it’s… *blurry*?

I still the first photo of my daughter, 35 minutes old, taken by my brother Claudio with a good old Nokia…

But really is Pixelated

> A common experience, right?

You zoom in, and suddenly, your majestic mountain range looks like someone stacked a bunch of LEGO bricks (or my daughter Minecraft screenshots…) and called it art. You want to frame it, print it, maybe even sell it on a mug… but no.

It’s stuck in the “too small to care” folder, forever.

I used to just accept it. “Well, that’s what happens with old phones,” I’d sigh, sipping my coffee like a defeated philosopher.

---

Then I remembered something: the terminal.

Yes, ***that* black screen with the blinking cursor** that looks like it’s judging you.

Remember **my last rant about how the command line is actually your best friend, not a relic from the 80s?**

Well, **today**, I’m putting my money (and my pixels) where my mouth is.

Let me introduce you to Real-ESRGAN — a mouthful of a name, but basically, it’s like giving your blurry images a pair of super-powered glasses. Or a time machine back to when they were crisp and full of life.

And guess what? You can run it from the terminal. In two commands.

> And my no GPU mini PC upscale my pictures in… 5 seconds!!!!

![](../assets/1_awmoOZxHGu0DOM5LcVNv7A.png)

*something went wrong here… that’s not my little girl!*

### Why the Terminal? Because it is a very obedient good boy

Look, I get it.

Clicking buttons feels safe. It’s like following a recipe with pictures. But the terminal? It’s like having a conversation with an obedient and friendly buddy who does *exactly* what you say — no guessing, no wandering through menus.

And with tools like Real-ESRGAN, that buddy becomes a photo wizard.

In the past (May 2024) I tried to create an app to give new life to my small images, but it was really a long long process, waiting time to load pytorch and other complex technicalities.

[**The ultimate DIY guide: Upscale your images 4x without limits**  
*Master the art of Upscaling and shatter the constraints to your creativity with AI on your Laptop*blog.stackademic.com](https://blog.stackademic.com/the-ultimate-diy-guide-upscale-your-images-4x-without-limits-346b4d12647a "https://blog.stackademic.com/the-ultimate-diy-guide-upscale-your-images-4x-without-limits-346b4d12647a")

---

But now… here’s the magic trick:

1. You have a tiny, sad, 480p image.
2. You type a command.
3. A few seconds later, you have a sharp, detailed 4K version.
4. You stare at it in disbelief. Then you high-five yourself. (I do. Don’t judge.)

And yes, it really is that simple — especially if you use the standalone pre-compiled binaries from the Real-ESRGAN project (or community forks). No Python, no dependencies, no crying over `pip install` errors.

[**GitHub - xinntao/Real-ESRGAN: Real-ESRGAN aims at developing Practical Algorithms for General…**  
*Real-ESRGAN aims at developing Practical Algorithms for General Image/Video Restoration. - xinntao/Real-ESRGAN*github.com](https://github.com/xinntao/Real-ESRGAN/ "https://github.com/xinntao/Real-ESRGAN/")

Just download, unzip, and run.

![](../assets/1_3rQWFRoTs7Wm7m5WWU7pJA.png)

*image by the author and Flux with this method*

### Let’s Upscale Something (Without Breaking the Internet)

Imagine you downloaded a cool anime poster, but it’s tiny. Or maybe you found an old family photo scanned at low quality. Here’s how you rescue it:

⬇️ Download the tool (like `realesrgan-ncnn-vulkan.exe` for Windows).

It is really easy: go to and download according to your Operating System. My guide is for Window, so here the related steps

![](../assets/1_gQd1LcIHnWwoFtb8jFrbuA.png)

*download page here*

💾 Click on Windows and wait for the file `realesrgan-ncnn-vulkan-20220424-windows.zip` to be downloaded (it is 43 Mb).

📂 Extract the ZIP archive in a folder (I usually keep the same filename)…

![](../assets/1_93mX8axcrHF80zYP1_ymhA.png)

💻 Now you have the entire working `upscaler` app already on your PC! Enter the directory and open the terminal.

![](../assets/1_bSq1f2Wp0NkWRBOndMZF3g.png)
> NOTE: there are already 5 small models in the `models` directory, so we really have nothing more to do!

```
realesr-animevideov3-x2.bin                                            
realesr-animevideov3-x3.bin                                            
realesr-animevideov3-x4.bin                                            
realesrgan-x4plus-anime.bin                                            
realesrgan-x4plus.bin
```

---

![](../assets/1_LSRBw7OGoZ0E_uRtZR1wzw.png)

✅ Put your blurry image in the same folder (let’s call it `grandma_love.png`—legendary moment, terrible resolution).

![](../assets/1_8c3RzduhwHviFS3YMTeskA.png)

*1170x1560 my grandma Maria*

✅ Open the terminal in that folder (Shift + Right-click > “Open Terminal Here”).

✅ Type this:

```
realesrgan-ncnn-vulkan.exe -i grandma_love.png -o grandma_love_UPSCALED2.png
```

Boom. Done.

- `-i` = input (your sad image)
- `-o` = output (your glorious new image)
- Wait a few seconds, and voilà!

![](../assets/1_co86d1aGBl7hIyxQVlhjlA.gif)

*no speedup here… 16 seconds*

Grandma is not just holding my daughter — she’s *holding her in HD*, with every wrinkle and joyful tear rendered in stunning detail.

---

If you want a more advanced upscale with higher capabilities (but much slower…) you can add the selection of the model:

```
realesrgan-ncnn-vulkan.exe -i grandma_love.png -o grandma_love_UPSCALED.png -n realesrgan-x4plus
```

- `-n` = which magic model to use (x4plus is great for general photos)

Wait a much more seconds, and voilà!

![](../assets/1_8uaNjhRAlKQu4EsBzJuRNQ.gif)

*here I had to speed up… 5 minutes and 31 seconds!!!*

We just upgraded her entire life in one command.

I created for my entertainment a quick `gradio` slider to evaluate the 2 pictures side by side…

![](../assets/1_u9YnEH-I_NNOUr3lMDbnFw.png)

### Why this beats clicking around

Let’s be real: most AI upscaling tools online want your email, your soul, or $9.99/month. Or they compress your image so much that you’re back to square one.

But with the terminal:

- No ads. No login. No nonsense.
- It’s free. Forever.
- You keep full control. The file never leaves your computer.
- You can batch-process 100 images with a simple loop (yes, you can even process an entire video and upascale it!).

And the best part? You’re not only using AI — you’re *talking* to it.

You’re not a passive user.

You’re the director. The wizard. The one holding the wand.

---

### But wait… isn’t the Terminal scary?

I used to think it was like opening the hood of a car and staring at the engine. “What if I touch the wrong thing and it explodes?”

But here’s the truth: you can’t break anything unless you *try*.

Type the wrong command? Nothing happens. Or it tells you “file not found” — which is just the computer’s way of saying, “Nice try, buddy.”

And every time you run a command and it works? You feel like a tiny bit of a hacker. A digital MacGyver.

But please… do not type:

```
format C:
```

---

![](https://cdn-images-1.medium.com/max/1200/0*o2lGKGIKE-j9SqA-)

### What’s next? Let’s make the Terminal smarter

Now, imagine combining this power with a simple Python script. Want a tool that:

- Asks you which image to upscale?
- Lets you choose between “photo” or “anime” mode?
- Automatically saves the result in an “upscaled” folder?

That’s just 10 lines of Python. No AI PhD. Just `input()`, `if` statements, and calling the same terminal command from code.

This is the future I love: humans in control, using simple tools to harness powerful AI. Not letting apps decide for us. Not uploading private photos to random servers.

Just you, your computer, and a little script that says: *“Let’s make this awesome.”*

### So Go Ahead — Open That Black Window

The terminal isn’t scary. It’s your secret weapon.

And Real-ESRGAN? It’s your magic wand.

Download it. Try it. Upscale something silly. Then something meaningful.

And when you see that blurry memory come to life in stunning clarity… you’ll realize something beautiful:

> You fixed a photo.  
> You reclaimed a moment.

Now go forth. Talk to your computer.  
And maybe — just maybe — teach it a few new tricks.

---

I hope you enjoyed the article. If this story provided value and you wish to show a little support, you could:

1. Clap a lot of times for this story
2. Highlight the parts more relevant to be remembered (it will be easier for you to find them later and for me to write better articles)
3. **Join my** [**totally free weekly Substack newsletter here**](https://thepoorgpuguy.substack.com/about)
4. Sign up for a Medium membership ($5/month to read unlimited Medium stories)
5. Follow me on Medium
6. Read my latest articles at <https://medium.com/@fabio.matricardi>
7. Follow my publication <https://medium.com/artificial-intel-ligence-playground>

If you want to read more, here are some ideas:

[**How to not waste 27 hours to send an email**  
*A quick and easy hack to get your AI projects sending emails with Python without all the hassle.*generativeai.pub](https://generativeai.pub/how-to-not-waste-27-hours-to-send-an-email-cf2ffbb0698a "https://generativeai.pub/how-to-not-waste-27-hours-to-send-an-email-cf2ffbb0698a")

[**Why your AI reply feels unpredictable (and the simple system that fixes it)**  
*In the end Structured Output is all you need — and here’s how you can do it on your PC*generativeai.pub](https://generativeai.pub/why-your-ai-reply-feels-unpredictable-and-the-simple-system-that-fixes-it-c4adcc70948f "https://generativeai.pub/why-your-ai-reply-feels-unpredictable-and-the-simple-system-that-fixes-it-c4adcc70948f")

[**What kind of Intelligence should AI have?**  
*Cool visions on new architectures, LLM optimizations, fine-tuning and paradigm shifts*pub.towardsai.net](https://pub.towardsai.net/what-kind-of-intelligence-should-ai-have-14502f8e9385 "https://pub.towardsai.net/what-kind-of-intelligence-should-ai-have-14502f8e9385")

[**How to use Mistral AI for FREE everywhere**  
*All European languages, image generation, coding assistant and much more with LeChat. And here is how to use it at no…*generativeai.pub](https://generativeai.pub/how-to-use-mistral-ai-for-free-everywhere-f3575755ac23 "https://generativeai.pub/how-to-use-mistral-ai-for-free-everywhere-f3575755ac23")