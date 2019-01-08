# Convert Code to Executable

1. Download pyinstaller
python console:
```
pip install pyinstaller
```

2. Change working directory to python script location
python console:
```
cd C:/path/to/your/python/files
```

3. Execute pyinstaller
python console:
```
pyinstaller --onefile --windowed chatbot.py
```
This bundles all of the scripts and data into one executable file in a `dist` folder in your working directory. Move the `chatbot_data.csv` file into the same place as the executable. When you run the program, the executable will initialize with that csv and your chatbot will work. 
