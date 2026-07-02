import feedparser
import httpx
import pathlib
import re
import os
import requests
import git

root = pathlib.Path(__file__).parent.resolve()

def replace_chunk(content, marker, chunk, inline=False):
    r = re.compile(
        r"<!\-\- {} starts \-\->.*<!\-\- {} ends \-\->".format(marker, marker),
        re.DOTALL,
    )
    if not inline:
        chunk = "\n{}\n".format(chunk)
    chunk = "<!-- {} starts -->{}<!-- {} ends -->".format(marker, chunk, marker)
    return r.sub(chunk, content)

def get_tils():
    til_readme = "https://raw.githubusercontent.com/milaan9/TIL/master/README.md"
    r = requests.get(til_readme)

    page = requests.get(til_readme)
    all_text = page.text
    search_re = re.findall( r'(\*+).(\[.*?\])(\(.*?\)).?-(.+)', all_text, re.M|re.I)
    dt_til = sorted(search_re, key=lambda search_re: search_re[3], reverse=True)[:3]
    
    til_md = ""
    
    for i in dt_til:
        til_md += "\n" + i[0] + ' ' + i[1] + i[2]         
       
    return til_md

def fetch_blog_entries():
    entries = feedparser.parse("https://milaan9.github.io/blog/feed.xml")["entries"]
    return [
        {
            "title": entry["title"],
            "url": entry["link"].split("#")[0],
            "published": entry["published"].split("T")[0],
        }
        for entry in entries
    ]


if __name__ == "__main__":

    readme = root / "README.md"
    readme_contents = readme.open().read()
    
    entries = fetch_blog_entries()[:3]
    entries_md = "\n".join(
        # ["* [{title}]({url}) - {published}".format(**entry) for entry in entries]
        ["* [{title}]({url})".format(**entry) for entry in entries]
    )
    rewritten = replace_chunk(readme_contents, "blog", entries_md)

    til_readme_contents = get_tils()
    rewritten = replace_chunk(rewritten, "tils", til_readme_contents)    
    
    readme.open("w").write(rewritten)






<h1 align="center">👋 Hi, I'm <span style="color:#00BFFF;">Atish Kumar Sah</span></h1>
<h3 align="center">💻 Full Stack Developer (MERN) | 🚀 Tech Enthusiast | 🌱 Lifelong Learner</h3>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=22&pause=1000&color=00BFFF&center=true&vCenter=true&width=600&lines=👨‍💻+B.Tech+in+Computer+Science+%26+Engineering;🌐+Full-Stack+Developer+(MERN);📚+Currently+learning+DSA+and+Open+Source;🚀+Building+impactful+projects+to+solve+real+problems!" />
</p>

---

## 🧑‍💻 Who Am I?

💡 **B.Tech CSE Student** at *Parul University, Gujarat*  
🚀 Passionate about **Full-Stack Web Development (MERN)**, **DSA-JAVA**  
🌱 Constantly exploring **new technologies** and building **impactful projects**  
🎯 Goal: To create scalable solutions that make a difference in the real world  

---

## 🧰 Skills & Tools

<p align="center">
  <img src="https://img.shields.io/badge/Code-HTML5-informational?style=flat&logo=html5&color=E34F26" />
  <img src="https://img.shields.io/badge/Code-CSS3-informational?style=flat&logo=css3&color=1572B6" />
  <img src="https://img.shields.io/badge/Code-JavaScript-informational?style=flat&logo=javascript&color=F7DF1E" />
  <img src="https://img.shields.io/badge/Framework-React-informational?style=flat&logo=react&color=61DAFB" />
  <img src="https://img.shields.io/badge/Backend-Node.js-informational?style=flat&logo=node.js&color=339933" />
  <img src="https://img.shields.io/badge/Database-MongoDB-informational?style=flat&logo=mongodb&color=47A248" />
  <img src="https://img.shields.io/badge/Framework-Express.js-informational?style=flat&logo=express&color=000000" />
  <img src="https://img.shields.io/badge/Version Control-Git-informational?style=flat&logo=git&color=F05032" />
  <img src="https://img.shields.io/badge/UI-Bootstrap-informational?style=flat&logo=bootstrap&color=7952B3" />
</p>

---

## 🧩 Projects That Define Me

1. **AgriConnect**  
   🌾 Smart platform empowering farmers with digital tools for productivity.  
2. **MERN Stack Apps**  
   💻 Building scalable web applications with modern tech stacks.  
3. **Open Source Contributions**  
   🤝 Collaborating to make the developer community stronger.  
4. **DSA**  
   🧠 Solving real-world algorithmic problems efficiently.

---

## 📊 GitHub Highlights

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=sahatish&show_icons=true&theme=tokyonight" alt="Atish's GitHub stats" height="180em"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=sahatish&layout=compact&theme=tokyonight" alt="Top Languages" height="180em"/>
</p>

<p align="center">
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=sahatish&theme=tokyonight" alt="GitHub Streak"/>
</p>

---

## 🌟 Fun Facts About Me

- 🧩 Love solving puzzles — whether in code or logic form  
- 💬 Believe in lifelong learning and sharing knowledge  
- 🌍 Dream of building tech that truly impacts lives  

---

## 🤝 Let's Connect!

<p align="center">
  <a href="https://github.com/sahatish">
    <img src="https://img.icons8.com/fluency/48/000000/github.png" alt="GitHub" />
  </a>
  <a href="mailto:sahatish1st456@gmail.com">
    <img src="https://img.icons8.com/fluency/48/000000/gmail.png" alt="Gmail" />
  </a>
  <a href="https://www.linkedin.com/in/atish-sah-8a1a9b260/">
    <img src="https://img.icons8.com/fluency/48/000000/linkedin.png" alt="LinkedIn" />
  </a>
</p>

---

<h4 align="center">✨ Thanks for visiting my profile! Let’s create something amazing together 🚀</h4>
    
