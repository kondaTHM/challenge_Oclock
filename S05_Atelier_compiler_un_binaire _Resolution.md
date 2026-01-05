# Compiler un binaire

Ok, on peut installer des binaires pré-compilés pour notre système grâce au gestionnaire de paquets de notre distribution.

Mais si le programme qu'on veut installer n'est pas disponible dans les dépôts ?

→ On va devoir le compiler nous-même !

## Langages de programmation

Il existe de nombreux langages de programmation qui peuvent être utiliser pour développer des binaires GNU/Linux.

On peut par exemple utiliser :

- C
- C++
- Rust
- Assembleur
- etc.

⚠️ Attention, certains langages comme Python par exemple, ne sont pas compilés mais **interprétés**.

Les langages C ou C++ sont très fréquemment utilisés. Si le binaire que vous voulez compiler a été codé dans un autre langage, il faudra suivre des instructions différentes.

## Compiler un programme C/C++

Les instructions ci-dessous ont été testées sur une distribution Debian 12.

### Notre premier programme en C

Plutôt que d'utiliser un programme trouvé sur Internet, et si on codait le notre ? Je vous rassure, on va faire simple : créons un `Hello world` en C.

Créons un nouveau dossier, puis un fichier `main.c` à l'intérieur.

```bash
cd ~
mkdir hello_world
cd hello_world
nano main.c
```

Contenu du fichier `main.c` :

```c
#include <stdio.h>

int main()
{
    printf("Hello world!\n");
    return 0;
}
```

Pour compiler ce fichier de code C, il nous faut un compilateur. Il en existe plusieurs, mais le plus connu et le plus utilisé est **gcc**.

#### Compilation

Sur Debian, on peut installer gcc avec la commande suivante :

```bash
sudo apt update
sudo apt install build-essential
```

💡 Le paquet `build-essential` contient tout ce qu'il faut pour compiler des programmes en C, donc `gcc` !

Une fois l'installation terminée, on peut compiler notre premier programme avec la commande :

```bash
gcc main.c -o hello
```

💡 L'argument `-o hello` nous permet de choisir le nom du fichier binaire généré.

#### Lancer le binaire

Pour lancer le binaire, on peut lancer la commande :

```bash
./hello
```

On devrait voir notre texte "Hello world!" s'afficher dans le terminal 🎉

⚠️ Attention, il faut être dans le dossier `~/hello_world` pour que la commande ci-dessus fonctionne.

Si on tape directement la commande `hello`, on aura une erreur `Command not found`. Or d'habitude, quand on installe un programme, on peut le lancer sans rajouter `./` devant, et sans devoir se placer dans un dossier spécifique !

### Path

Ce problème est lié à la notion de **Path**.

Path est un terme anglais qui se traduit en "chemin", mais quand on parle de Path en informatique, on fait souvent référence à une variable système utilisée pour indiquer l'emplacement des fichiers binaires, des programmes installés.

Sur GNU/Linux, on peut afficher le contenu de cette variable avec la commande :

```bash
echo $PATH
```

Vous devriez obtenir quelque-chose comme `/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games`.

Sur notre système, les binaires sont donc dans l'un des dossiers suivants :

- /usr/local/bin
- /usr/bin
- /bin
- /usr/local/games
- /usr/games

Si on veut pouvoir lancer directement notre programme, il faut donc qu'on copie le binaire généré par gcc dans l'un de ces dossiers, par exemple avec la commande :

```bash
sudo cp hello /usr/bin/
```

⚠️ Attention, il faut être dans le dossier `~/hello_world` pour que la commande ci-dessus fonctionne.

On peut maintenant lancer directement notre programme, depuis n'importe quel dossier, avec la commande `hello`.

### Et en C++ ?

On peut réécrire le même programme en C++, dans un fichier `hello.cpp` par exemple :

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World!\n";
    return 0;
}
```

On peut le compiler avec la commande :

```bash
gcc hello.cpp -lstdc++ -o hello_cpp
```

Puis le lancer avec la commande :

```bash
./hello_cpp
```

> Pourquoi on doit rajouter `-lstdc++` à la commande `gcc` ?

Pour écrire du texte dans la console en C++, on utilise la fonction `cout`, qui fait partie de la bibliothèque standard C++. Cette bibliothèque n'est pas liée automatiquement par `gcc` lors de la compilation : on doit indiquer qu'on veut lier cette bibliothèque **explicitement**.

## Les bibliothèques

Quand on code un programme, on essaye de ne pas réinventer la roue ! On réutilise des morceaux de code déjà écrits par d'autres développeurs.

Ces morceaux de code sont disponibles dans des **bibliothèques** (library, en anglais).

Il existe des tonnes de bibliothèques, qui permettent de faire diverses choses :

- créer des interfaces graphiques
- faire des opérations mathématiques poussées
- créer des jeux vidéos 2D/3D
- communiquer sur le réseau
- etc.

Prenons un exemple : installons la bibliothèque SDL (qui permet de faire des jeux 2D) et essayons de compiler un programme de démo.

### Installer SDL

La bibliothèque SDL est disponible dans les dépôts officiels Debian, on peut l'installer avec la commande :

```bash
sudo apt install libsdl2-dev
```

💡 Les paquets dont le nom commence par `lib...` sont en général des bibliothèques.

### Premier programme avec SDL

```cpp
#include <SDL.h>
#include <iostream>

const int SCREEN_WIDTH = 800;
const int SCREEN_HEIGHT = 600;

int main(int arc, char ** argv) {
    SDL_Window* window;
    SDL_Renderer* renderer;
    
    if (SDL_Init( SDL_INIT_VIDEO ) < 0) {
        std::cout << "SDL could not initialize! SDL_Error: " << SDL_GetError() << std::endl;
    } else {
        
        window = SDL_CreateWindow(
            "SDL2 Demo",
            SDL_WINDOWPOS_CENTERED, SDL_WINDOWPOS_CENTERED,
            SCREEN_WIDTH, SCREEN_HEIGHT,
            SDL_WINDOW_SHOWN
        );
        
        renderer = SDL_CreateRenderer(window, -1, 0);
        
        // Select the color for drawing. It is set to red here.
        SDL_SetRenderDrawColor(renderer, 255, 0, 0, 255);
        
        // Clear the entire screen to our selected color.
        SDL_RenderClear(renderer);
        
        // Up until now everything was drawn behind the scenes.
        // This will show the new, red contents of the window.
        SDL_RenderPresent(renderer);
        
        SDL_Delay(2000);
    }
    
    return 0;
}
```

#### Compilation

Pour compiler notre programme ci-dessus, il faut lancer la commande suivante :

```bash
gcc main.cpp -o sdl_demo -lstdc++ `sdl2-config --cflags --libs`
```

Ça se complique 😬

Et comme précédemment, on peut lancer le programme compilé avec `./sdl_demo`.

Une fenêtre noire devrait s'ouvrir, puis se refermer au bout de 2 secondes (grâce à la ligne de code `SDL_Delay(2000)`).

### Deuxième programme avec SDL & SDL_Image

Facultatif !

Contenu du fichier `main.cpp` :

```cpp
#include <SDL.h>
#include <SDL_image.h>

int main(int argc, char *argv[])
{
    // returns zero on success else non-zero
    if (SDL_Init(SDL_INIT_EVERYTHING) != 0) {
        printf("error initializing SDL: %s\n", SDL_GetError());
    }
    SDL_Window* win = SDL_CreateWindow("GAME", // creates a window
                                       SDL_WINDOWPOS_CENTERED,
                                       SDL_WINDOWPOS_CENTERED,
                                       1000, 1000, 0);
    
    // triggers the program that controls
    // your graphics hardware and sets flags
    Uint32 render_flags = SDL_RENDERER_ACCELERATED;
    
    // creates a renderer to render our images
    SDL_Renderer* rend = SDL_CreateRenderer(win, -1, render_flags);
    
    // creates a surface to load an image into the main memory
    SDL_Surface* surface;
    
    // please provide a path for your image
    surface = IMG_Load("./Tux.png");
    
    // loads image to our graphics hardware memory.
    SDL_Texture* tex = SDL_CreateTextureFromSurface(rend, surface);
    
    // clears main-memory
    SDL_FreeSurface(surface);
    
    // let us control our image position
    // so that we can move it with our keyboard.
    SDL_Rect dest;
    
    // connects our texture with dest to control position
    SDL_QueryTexture(tex, NULL, NULL, &dest.w, &dest.h);
    
    // adjust height and width of our image box.
    dest.w /= 6;
    dest.h /= 6;
    
    // sets initial x-position of object
    dest.x = (1000 - dest.w) / 2;
    
    // sets initial y-position of object
    dest.y = (1000 - dest.h) / 2;
    
    // controls animation loop
    int close = 0;
    
    // speed of box
    int speed = 300;
    
    // animation loop
    while (!close) {
        SDL_Event event;
        
        // Events management
        while (SDL_PollEvent(&event)) {
            switch (event.type) {
                case SDL_QUIT:
                    // handling of close button
                    close = 1;
                    break;
                
                case SDL_KEYDOWN:
                    // keyboard API for key pressed
                    switch (event.key.keysym.scancode) {
                        case SDL_SCANCODE_W:
                        case SDL_SCANCODE_UP:
                            dest.y -= speed / 30;
                            break;
                        case SDL_SCANCODE_A:
                        case SDL_SCANCODE_LEFT:
                            dest.x -= speed / 30;
                            break;
                        case SDL_SCANCODE_S:
                        case SDL_SCANCODE_DOWN:
                            dest.y += speed / 30;
                            break;
                        case SDL_SCANCODE_D:
                        case SDL_SCANCODE_RIGHT:
                            dest.x += speed / 30;
                            break;
                        default:
                            break;
                    }
            }
        }
        
        // right boundary
        if (dest.x + dest.w > 1000)
            dest.x = 1000 - dest.w;
        
        // left boundary
        if (dest.x < 0)
            dest.x = 0;
        
        // bottom boundary
        if (dest.y + dest.h > 1000)
            dest.y = 1000 - dest.h;
        
        // upper boundary
        if (dest.y < 0)
            dest.y = 0;
        
        // clears the screen
        SDL_RenderClear(rend);
        SDL_RenderCopy(rend, tex, NULL, &dest);
        
        // triggers the double buffers
        // for multiple rendering
        SDL_RenderPresent(rend);
        
        // calculates to 60 fps
        SDL_Delay(1000 / 60);
    }
    
    // destroy texture
    SDL_DestroyTexture(tex);
    
    // destroy renderer
    SDL_DestroyRenderer(rend);
    
    // destroy window
    SDL_DestroyWindow(win);
    
    // close SDL
    SDL_Quit();
    
    return 0;
}
```

Avant de compiler, il faut installer une lib en plus & télécharger une image :

```bash
sudo apt install libsdl2-image-dev
wget https://upload.wikimedia.org/wikipedia/commons/a/af/Tux.png
```

Puis pour compiler :

```bash
gcc main.cpp -o sdl_demo2 -lstdc++ `sdl2-config --cflags --libs` -lSDL2_image
```

## Make & makefile

Juste en rajoutant une bibliothèque, on voit que la commande pour compiler se complique nettement. Pas très pratique …

Parfois, il faut également compiler plusieurs fichiers (donc potentiellement plusieurs commande `gcc` à lancer).

Parfois, il faut utiliser un compilateur différent.

> Pfiou, la galère …

On peut simplifier la compilation en utilisant un `makefile` !

Ce fichier va décrire les différentes commandes à lancer pour compiler notre programme, l'installer, et bien plus encore !

Créons un `makefile` basique pour notre Hello World en C :

```bash
cd ~/hello_world
nano makefile
```

Contenu du `makefile` :

```makefile
CC = gcc

default: all

all: main.c
	$(CC) -o out main.c

install:
	cp out /usr/bin/hello
```

On peut ensuite lancer la compilation avec la commande :

```bash
make
```

Puis installer notre programme dans le bon dossier avec la commande :

```bash
sudo make install
```

💡 La plupart des programmes disposent d'un `makefile`.

## Compiler un programme existant

Essayons de compiler le programme `cmatrix`.

```bash
cd ~
wget https://github.com/abishekvashok/cmatrix/releases/download/v2.0/cmatrix-v2.0-Butterscotch.tar
tar -xvf cmatrix-v2.0-Butterscotch.tar 
cd cmatrix

./configure
make

# Erreur, libs/dépendances manquantes :
sudo apt install autoconf
sudo apt install libncurses5-dev libncursesw5-dev

make
sudo make install

cmatrix
```

La commande `./configure` permet de générer un makefile approprié à notre environnement courant. Ce fichier est un script Bash, généré automatiquement avec le logiciel GNU autoconf.
