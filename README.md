# **Шпаргалка: Создание и синхронизация локального и удалённого репозиториев**

**Git** — это

система контроля версий, которая помогает отслеживать изменения в проекте.  
Git позволяет сохранять изменения локально и при необходимости возвращаться к предыдущим версиям проекта. Также можно создать удалённую копию на хостинг-платформе, которая работает с Git, и поделиться результатом с другими.

---

# **Локальный репозиторий**

## **Создание и инициализация репозитория**

1. создайте папку *"Название_папки"* с помощью команды ```touch```.
2. перейдите в неё с помощью команды ```cd```.
3. выполните команду ```git init```.  

Ура! вы создали и инициализировали репозиторий.  
С помощью команды ```git status``` можно смотреть статус репозитория.  


«Разгитить» папку (т.е. удалить скрытую папку *.git*), если что-то пошло не так, можно с помощью команды ```rm -rf .git```, перейдя предварительно в папку с помощью команды ```cd```.  

### **Добавление файлов в репозиторий**

1. создайте в папке репозитория файлы с помощью команды ```touch```.
2. подготовьте к сохранению файлы с помощью команды:
- ```git add --all``` для всех файлов сразу,
- ```git add <*название файла*>``` для отдельного файла,
- ```git add .``` для текущей папки.
3. проверьте статус с помощью команды ```git status```, чтобы посмотреть, что изменилось.  

Готово! Файлы, которые отмечены зелёным, теперь отслеживаются и готовы к сохранению.  

### **Сохранение состояния файлов в репозитории**

Сохранение, или фиксацию состояния файлов, называют **коммитом**. Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». По аналогии с командой Ctrl+Z для целой папки (репозитория).  
1. перейдите в папку репозитория и создайте коммит с помощью следующей команды: ```$ git commit -m "текст-описание для коммита"```.
2. с помощью команды ```git commit``` выведите информацию о коммите.

---

# **Создание удалённого репозитория на GitHub**

1. войдите в свой акк на GitHub и во вкладке *Repositories* нажмите на зеёлную кнопку **New** справа.
2. в окне создания нового репозитория назовите его и нажмите **Create repository**.  

Ура! вы создали удалённый репозиторий  
Осталось связать его с локальным - тем, что уже есть на компьютере.

---

# **Синхронизация репозиториев**

## **1. Генерация SSH-ключа**

1. откройте терминал и введите команду: ```ssh-keygen -t ed25519 -C "электронная почта, к которой привязан аккаунт на GitHub"``` ИЛИ команду ```ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан аккаунт на GitHub"```.
2. дважды нажмите **Enter **.  

Готово!  
Вызовите команду ```ls -a ~/.ssh```, чтобы проверить, сгенерировались ли ключи.  
На экране должны появиться два файла — один с расширением .pub, другой — без.  
Файл в .pub — публичный, им можно делиться с веб-сайтами или коллегами.  
**Файл без расширения .pub — приватный, им делиться нельзя!**


## **2. Связывание SSH-ключа и GitHub-аккаунта**

1. выведите содержимое файла **.pub** с помощью ```cat ~/.ssh/id_rsa.pub``` или ```cat ~/.ssh/id_ed25519.pub```.
2. скопируйте содержимое файла с публичным ключом (расширение **.pub**).
3. перейдите на GitHub и выберите пункт **Settings** в меню аккаунта.
4. в меню слева нажмите на пункт **SSH and GPG keys**, в открывшейся вкладке выберите **New SSH key**.
5. заполните окно **SSH-keys/Add new**: 
- в поле **Title** придумайте и впишите название ключа.
- в поле **Key type** должно быть **Authentication Key**.
- в поле **Key** скопируйте ваш ключ из буфера обмена.  
Нажмите на кнопку **Add SSH key**.
6. перейдите в консоль и проверьте правильность ключа с помощью команды ```ssh -T git@github.com```.  
Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Если ключ в предупреждении совпадает с тем, что вы видите на сайте, значит, сервер является действительным. 
7. введите **yes**, чтобы продолжить. появится приветствие на экране.  

Ура! ваш ключ привязан к GitHub!

## **3. Связывание локального и удалённого репозиториев**

1. перейдите на страницу удалённого репозитория на GitHub, выберите тип SSH и скопируйте URL.
2. откройте консоль, перейдите в каталог локального репозитория с помощью команды ```cd```.
3. введите команду ```git remote add origin <URL>```.
4. убедитесь, что всё работает, с помощью команды ```git remote -v```. В выводе вы должны увидеть две строчки c (fetch) и (push) на конце.  

Локальный и удалённый репозитории связаны! 

## **4. Синхронизация локального и удалённого репозиториев**

1. загрузите содержимое локального репозитория на GitHub с помощью команды ```git push -u origin main``` *(если команда приведёт к ошибке, попробуйте заменить main на master)*. 
2. зайдите в репозиторий на GitHub - в репозитории появились файлы с изменениями.  
В дальнейшем при работе с удалённым репозиторием флаг ```-u``` можно опустить и писать просто ```git push```.  

Ура! Локальный и удалённый репозитории синхронизированы!

