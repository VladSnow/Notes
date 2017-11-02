## Немного о GIT

* Установите Git (на Linux)  
`sudo apt-get install git`  

* Нужно задать (сконфигурировать) свое имя и свой email  
**git config --global user.name "your_name"**  
**git config --global user.name your_email**  

* Клонирование репозитория из github к себе локально  
**git clone your_link**  
(example: git clone https://github.com/VladSnow/notes)  
---
* инициализируем  git  
**git init**  

* добавить все файлы в git  
**git add --all**  

* проверить статус  
**git status**  

* закоммитить файлы  
**git commit -m "your_message"**  

* задать путь к репозиторию на github  
**git remote add your_title your_link_github**  
(example: git remote gitProject https://github.com/VladSnow/notes)  

* посмотреть удаленные репозитории  
**git remote**  

* заливаем проект по заданному пути  
**git push your_title master**  
(example: git push gitProject master)  
---
* задать версию проекта  
**git tag "your_message"**  
(example: git tag "version_1.0")  

* добавить новую ветку (от основной)  
**git branch your_branch_title**  
(example: git branch newBranch)  

* перемещение в нужную ветку  
**git checkout your_branch_title**  
(example: git checkout newBranch)  

* проверить в какой ветке находимся в данный момент  
**git branch**  

* слияние веток (когда находимся в мастере)  
**git merge your_branch_title**  
(example: git merge newBranch)  

* посмотреть историю изменений git  
**git log**  

---

[спека для создания файла .gitignore](https://orlov.io/ru/articles/podrobnee-o-faile-gitignore) 