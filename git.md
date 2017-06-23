# 关于git push的一些知识

## git里面的origin到底啥意思？

你的代码库(repository)可以存放在你的电脑里，同时你也可以把代码库托管到Github的服务器上。在默认情况下，origin指向的就是你本地的代码库托管在Github上的版本。我们假设你首先在github上创建了一个Repository，叫做repository，假设你的Github ID是user1,这个时候指向你的代码库的链接是https://github.com/user1/repository
如果你在terminal里输入git clone https://github.com/user1/repository
那么git就会在本地拷贝一份托管在github上的代码库这个时候你cd到repository然后输入git remote -v
你会看到控制台输出origin https://github.com/user1/repository.git (fetch)
origin https://github.com/user1/repository.git (push)
也就是说git为你默认创建了一个指向远端代码库的origin（因为你是从这个地址clone下来的）再假设现在有一个用户user2 fork了你个repository，那么他的代码库链接就是这个样子https://github.com/user2/repository
如果他也照着这个clone一把，然后在他的控制台里输入git remote -v
他会看的的就是origin https://github.com/user2/repository.git (fetch)
origin https://github.com/user2/repository.git (push)
可以看的origin指向的位置是user2的的远程代码库这个时候，如果user2想加一个远程指向你的代码库，他可以在控制台输入git remote add upstream https://github.com/user1/repository.git
然后再输入一遍 git remote -v输出结果就会变为origin https://github.com/user2/repository.git (fetch)
origin https://github.com/user2/repository.git (push)
upstream https://github.com/user1/repository.git (push)
upstream https://github.com/user1/repository.git (push)
增加了指向user1代码库的upstream，也就是之前对指向位置的命名。总结来讲，顾名思义，origin就是一个名字，它是在你clone一个托管在Github上代码库时，git为你默认创建的指向这个远程代码库的标签， @陈肖恩的答案并不准确，origin指向的是repository，master只是这个repository中默认创建的第一个branch。当你git push的时候因为origin和master都是默认创建的，所以可以这样省略，但是这个是bad practice，因为当你换一个branch再git push的时候，有时候就纠结了
