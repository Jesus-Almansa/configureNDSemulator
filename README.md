# 🍉 melonDS en Ubuntu 24

Guía completa para instalar y configurar el emulador **melonDS** en Ubuntu 24, con alias, acceso directo con icono personalizado y configuración de la ruta de guardado.  

---

## 🚀 1. Instalar dependencias

```bash
sudo apt update
sudo apt install build-essential cmake qtbase6-dev qtbase6-private-dev \
qtmultimedia6-dev libqt6svg6-dev libsdl2-dev libgtk-3-dev git
````

---

## 📥 2. Descargar el repositorio de melonDS

```bash
git clone https://github.com/melonDS-emu/melonDS
cd melonDS
```

---

## 🛠 3. Compilar melonDS

```bash
cmake -B build
cmake --build build -j$(nproc --all)
```

El ejecutable estará en `build/melonDS`.

---

## 💻 4. Crear un alias (opcional)

Para ejecutar melonDS desde cualquier terminal con `melonds`:

```bash
nano ~/.bashrc
```

Añade al final:

```bash
alias melonds='/home/tu_usuario/melonDS/build/melonDS'
```

Aplica los cambios:

```bash
source ~/.bashrc
```

Ahora puedes ejecutar:

```bash
melonds
```

---

## 🏠 5. Acceso directo en el menú

1. Crea la carpeta de aplicaciones si no existe:

```bash
mkdir -p ~/.local/share/applications
```

2. Crea el archivo `.desktop`:

```bash
nano ~/.local/share/applications/melonds.desktop
```

3. Pega lo siguiente (ajusta rutas):

```ini
[Desktop Entry]
Name=melonDS
Comment=Emulador de Nintendo DS
Exec=/home/tu_usuario/melonDS/build/melonDS
Icon=/home/tu_usuario/Imágenes/iconos/poke-ball.png
Terminal=false
Type=Application
Categories=Game;Emulator;
StartupNotify=true
StartupWMClass=net.kuribo64.melonDS
```

4. Hazlo ejecutable:

```bash
chmod +x ~/.local/share/applications/melonds.desktop
```

5. Actualiza la base de datos de menús:

```bash
update-desktop-database ~/.local/share/applications/
```

✅ Ahora melonDS aparecerá en el menú y podrás anclarlo al dock/barra de tareas con el icono correcto.

---

## 💾 6. Configurar la ruta de guardado en `melonDS.toml`

Por defecto, los save files (`.sav`) se guardan en la carpeta del ejecutable, pero puedes definir una carpeta específica en el archivo de configuración `melonDS.toml`:

1. Abre el archivo:

```bash
nano ~/.config/melonDS/melonDS.toml
```

2. Busca la sección `[Instance0]` y ajusta la ruta:

```toml
[Instance0]
SaveFilePath = "/home/usuario/MemoryCard/NDS"
EnableCheats = true
JoystickID = 0
SavestatePath = ""
CheatFilePath = ""
```

* `SaveFilePath` → carpeta donde se guardarán los archivos de guardado (`.sav`).
* `SavestatePath` → carpeta opcional para savestates.

3. Guarda y cierra (`Ctrl+O`, `Ctrl+X`).

Ahora todos los guardados de tus ROMs se crearán en la carpeta que definiste.

---

## 🔧 7. Notas adicionales

* Si el icono sigue mostrando un engranaje en la barra de tareas, verifica el `StartupWMClass` con:

```bash
xprop | grep WM_CLASS
```

y haz clic en la ventana de melonDS para obtener el valor correcto.

* `StartupWMClass` debe coincidir con lo que reporte Qt para que el icono y nombre aparezcan correctamente en la barra de tareas.

* Para cambiar otras configuraciones, revisa el archivo `melonDS.toml` en `~/.config/melonDS/`.

---