---
layout: post
title:  "Film Catalog"
date:   2021-06-25 12:19:54 -0300
categories: jekyll update
---
## About this project
The idea for this project emerged from the need I felt to create something big, that unites the things I know about SQL with all I learnt from Python. As a result, the **Film Catalog** emerged. A program which saves all the movies you want in a database, with a lot of flexibility over the tags you wanna put to the film. You can tag the movie you are inserting as: *to watch*, *already seen*, *top*, *worst*. You can select in which country the movie was made and at what genre it belongs. There is also the possibility to write a personal description of what you felt about the movie. Last you can rate it as you want.

This tags, not only belong to the movie, just as a tag, but are also filters. Imagine you have a thousand of movies in your personal catalog. In order to save time, you can just click the *to watch* button, and it will automatically select only the movies that have this tag on.

The **objective** is to answer the question that often comes from a friend, *Do you have any movies to recommend?*. This questions will not be unanswered anymore. You just tell him *wait a sec*. Then you enter into your personal catalog, search for the top movies you have ever seen, and there you go.

*What did I need for this project?*

To make this idea come alive I needed several things:
- A language, in this case Python.
- An UI module, which in this case I used *pygame*. Further in this post I will explain why is not a good idea programming an UI with pygame.
- A module to connect the program to a database. I chose **SQL Alchemy**.
- An SQL motor to run all the actions you wanna do to the database.

A part from this there are alse the screens.
Let's go step by step, screen by screen, shall we?
- Login window
- Sign-up window
- Main menu screen
- New movie window
- Edit window

## The login window
![image](Images/login_film.png){: width="500" }

The Login screen is pretty simple, as there are only 3 things that can interact with the user. 2 of them are textboxes, the one to write the username and the other one to write the password

The password will be shown like this:

![image](Images/password_film.png){: width="500" }

The other thing that can interact with the user is the text at the bottom right part of the window. If the text get pressed, it will redirect you to the *sign-up* window.

The logic behind this window, can be divided in 2:
- The UI logic.
- The Database logic.

The first one is pretty simple, so I won't explain anything about that.
The second one is also quite simple, but worth of some explanation.

*How does it work?*

Well, through `SQL Alchemy` for the logic of the Login, we need to create 1 table, the user one. Then, once the username and the password are in the database (these 2 things are inserted through the sign-up window), a function called *enter_mechanics* does the rest. It registers what the user entered and compares that information to the username and their passwords in the database. If the comparison is correct, it lets you go to the main menu, instead if something is wrong, an error message pops out.

## The sign-up window
![image](Images/sign_up_film.png){: width="500" }

The Sign-up window is pretty similar to the *login* window. The differences are 2:
- There are two passwords fields. One to wirte it down and the other one to confirm it.
- The window doesn't read from the database, instead it inserts the infromation.

The logic behind the insertion of information dosen't need much explanation, as it is just an insert of 2 things into to designated columns.

## The main menu screen
![image](Images/main_menu_film.png){: width="500" }

The main screen, is the core of all the program. The things you can do here are:
- See in a comfortable display all the movies you have in the database.
- Apply filters to narrow the searchs.
- Exit the program obviously.
- By clicking on a movie, go to the edition window of the movie.
- Go to the window to create a new movie by clinking on the *add new* button.

The logic behind the filters is really important, because it's one of the main functions of the program. Basically when you touch a filter, it calls a function from the class **DbManager**, located in the `Database_Manager` folder. The parameter you pass to it (which is a number) decides which filter you want to apply. once the function is called, it does the following things in order:
- It gets the ID of the logged in user.
- It gets all the movies of the user, not every movie in the database.
- Through the parameter, applies the correct filter. For example if you pressed the *to watch* button, it will search in the database for all the movies that have the *to watch* field with an 1 (1 = True, 0 = False).
- Then it creates a set of the two lists, to get the duplicates. These ones will be both the movies of the working user, and the movies with the filter applied.
- The rest is quite simple. It just gets the names of the movies through the IDs and the genre names.

This explanation works with the filters: *to watch*, *already seen*, *top*, *worst*.
The 2 other filters (the genre one and the country one) work in a different way. As the logic from these last two is almost the same as the other filters, it's only worth to explain where these two difer with the other ones.

The genre filter, instead of searching by the bit range of the selected column, it works with the parameter you pass to the function, that is the genre itself. For example if the parameter (because you clicked in the *action* button) is action, then the function will get the id of the genre (in this case ACC), it will get all the genres IDs from all the movies, and then filter the ones that are the genre id you selected (ACC). Once this is all done, it will get all the IDs of the movies that have the same genre ID, and finally create a set to get the duplicates within all the movies in the db with the genre filter you applied, and the ones the user have.

After this, the *genre_filter* function works the same way as the other filters function.

The country filter is simplier than the genre one. It just register the user input (for example USA) and filters all the movies by this country ID. Then get the set, and etc.

The more challenging part about creating this menu was for sure the display of the movies. From the beginning I was avoiding this part, but at the end i got no choice. So the problem, if you want to think about it, would be seomthing like this:

*How can you display all the movies on the screen, and make it interactive?*

I had really wild ideas. Like making a scroll view, using an external program, mixing pygame with Qt5 or giving up. I tried different things but at the end I managed to solve the problem with the function called *init movies*.

This is the code for the function:

```
def init_movies(self):
        self.movies_list.clear()
        Movies.movies_list_temp.clear()
        if self.index < len(e.movies_display_name):    
            self.movie = Movies("Images/movies_rect.png", (290, 120), (300, 130), (300, 230), e.movies_display_name[self.index], e.movies_display_genre_name[self.index])
        self.index += 1
        if self.index < len(e.movies_display_name):  
            self.movie2 = Movies("Images/movies_rect.png", (540, 120), (550, 130), (550, 230), e.movies_display_name[self.index], e.movies_display_genre_name[self.index])
        self.index += 1
        if self.index < len(e.movies_display_name):  
            self.movie3 = Movies("Images/movies_rect.png", (800, 120), (810, 130), (810, 230), e.movies_display_name[self.index], e.movies_display_genre_name[self.index])
        self.index += 1
        if self.index < len(e.movies_display_name):  
            self.movie4 = Movies("Images/movies_rect.png", (290, 450), (300, 460), (300, 560), e.movies_display_name[self.index], e.movies_display_genre_name[self.index])
        self.index += 1
        if self.index < len(e.movies_display_name):  
            self.movie5 = Movies("Images/movies_rect.png", (540, 450), (550, 460), (550, 560), e.movies_display_name[self.index], e.movies_display_genre_name[self.index])
        self.index += 1
        if self.index < len(e.movies_display_name):  
            self.movie6 = Movies("Images/movies_rect.png", (800, 450), (810, 460), (810, 560), e.movies_display_name[self.index], e.movies_display_genre_name[self.index])
        else:
            pass

        for i in Movies.movies_list_temp:
            self.movies_list.append(i)
```

Let's go step by step on this one. 

The movies that will be displayed are 6, that's why there are 6 *self.movie*. The way it functions is more or less like this. Where the main menu window function opens up, it creates a variable name *self.index*, which will be use to index a list of all the movies selected. Then you corroborate if the index is smaller than the length of the list with all the movies (this avoids the error of creating a movie without a name or something else). Once this is done, the index get a plus 1, so it reads the following movie in the list. That's the whole logic.

You maybe will be wondering, *What does that magical class called Movies?*. That class is the graphical part of the logic. It just creates a rectangle with the name of the movie and the genre name in it.

The list at the bottom is used to blit all the movies on screen. That's also why we gotta clear the list at the beginning of the function.

Other than this display, there was not much trouble creating the buttons and making them work.

## The new movie window
![image](Images/new_movie_film.png){: width="500" }

This window is the one where you create a movie. All the options you can put on the movie are not in this window, just beacuse I thought it would be easier for me and the user, to keep it simplier at the beginning. Once you created the film, if you want to put more attributes to it, you will need to edit it.

This particular window, that seems so innocent, so simple, was a torture to create. The description textbox had the whole fault, but, *Why?*.

Let's begin telling a little bit about pygame. This module is great to create a game, it has all you need, but it's not made, I repite, it's **NOT** made to create a great UI. The reason is quite simple, when you want to create an UI, you want the simple stuff to be already done, like the buttons. In pygame you gotta do every button by yourself from scratch. This means registering all the events on the screen, getting when the user pressed the mouse, getting where the user pressed the mouse, wich button is pressed and what does that button do. There are things to make it simplier, but overall it's not good for UI creation.

So imagine if creating a button is that hard (by hard I mean that you have a lot of things to worry about), *how hard could it be to create a notepad's type textbox?*

The answer for me at least was **HARD**.

The code for the working of the description textbox is this:

```
def description_mechanics(self):    
    if self.event.key == pygame.K_BACKSPACE and self.description_text.state:
        self.description_list[self.index].text = self.description_list[self.index].text[:-1]
        if self.index < 15 and len(self.description_list[self.index].text) == 0 and self.index != 0:
            self.index -= 1
    elif self.description_text.state and len(self.description_list[self.index].text) < 61:
        self.description_list[self.index].text += self.event.unicode
    elif len(self.description_list[self.index].text) > 59 and self.index < 15 and self.description_text.state:
        self.index += 1
```

It doesn't feel like it's hard to imagine this logic. For me, creating a from scratch logic to get a working textbox with different lines and different types of commands (like when you press backspace and there are no more letters in that line, so you go to the upper one) was pretty hard. In the code I'm showing you, the enter, backspace and tab mechanics are not included. 

This logic wasn't the worst part, the worst part began after I created this logic, when I have to fight against, at least 20 different bugs, which had no explanation at all. These bugs generated because pygame is not created for these types of work.

After solving all this, finally I got a working window where you can add the movie you want. The connection with the database is quite easy. You just insert all the data the user wrote, and manage the errors.

## The edit window
![image](Images/edit_film.png){: width="500" }

This is the last window I created and it wasn't really hard to do, as it's almost a copy of the *New movie* one. The thing I added in comparison to the other one are the 5 buttons you can see on the image, which work as filters or to delete the movie. 

## Wanna try it out yourself?

Unfortunatly you can't test this program, due to the fact that is connected to a local database in my computer. This database runs with a motor that cannot be distributed. There is also no way for me to host for other people around the world, as my computer is not turned on all day. The only solution is to pay a server, which currently I'm not willing to do. Anyways you can see the project's code in [My Github](https://github.com/Luulas-bot/Film_Catalog.git). I will also upload a video soon, showing how everything works together. 

