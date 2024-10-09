# Creating-GUI-to-Extract-Lyrics-from-Songs-Using-Python
import tkinter as tk
import requests
from tkinter import messagebox
class LyricsExtractor:
    def __init__(self, master):
        self.master = master
        master.title("Lyrics Extractor")
        master.geometry("400x300")
        self.song_label = tk.Label(master, text="Song Name:")
        self.song_label.pack()
        self.song_entry = tk.Entry(master, width=50)
        self.song_entry.pack()
        self.artist_label = tk.Label(master, text="Artist:")
        self.artist_label.pack()
        self.artist_entry = tk.Entry(master, width=50)
        self.artist_entry.pack()
        self.extract_button = tk.Button(master, text="Extract Lyrics", command=self.extract_lyrics)
        self.extract_button.pack()
        self.lyrics_text = tk.Text(master)
        self.lyrics_text.pack()

    def extract_lyrics(self):
        song_name = self.song_entry.get()
        artist_name = self.artist_entry.get()
        api_key = "YOUR_API_KEY_HERE"
        base_url = "https://api.lyrics.ovh/v1/"
        url = f"{base_url}{artist_name}/{song_name}"
        response = requests.get(url)
        data = response.json()
        if "lyrics" in data:
            lyrics = data["lyrics"]
            self.lyrics_text.delete(1.0, tk.END)
            self.lyrics_text.insert(tk.END, lyrics)
        else:
            messagebox.showerror("Error", "Lyrics not found!")
root = tk.Tk()
my_gui = LyricsExtractor(root)
root.mainloop()
