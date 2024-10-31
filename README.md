# Morse-code C#

This Program allows you to enter a string and encode it into Morse code, using ‘ . ‘ and ‘ - ‘ notation. Spaces between words should be replaced with the “|” (pipe) character.
Use a normal space for gaps between each character.
You can also translate from Morse to alphanumeric, using the standards above.

    using System;
    using System.Collections.Generic;
    using System.ComponentModel;
    using System.Data;
    using System.Drawing;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows.Forms;
    
    namespace Morse_code
    {
        public partial class Form1 : Form
        {
             private readonly Dictionary<char, string> morse_code = new Dictionary<char, string>
                {
                    { 'a' , " .-"  }, { 'b', " -... " }, { 'c', " -.-. " }, { 'd', " -.. " },
                    { 'e', " . " }, { 'f', " ..-. " }, { 'g', " --. " }, { 'h', " .... " },
                    { 'i', " .. " }, { 'j', " .--- " }, { 'k', " -.- " }, { 'l', " .-.. " },
                    { 'm', " -- " }, { 'n', " -. " }, { 'o', " --- " }, { 'p', " .--. " },
                    { 'q', " --.- " }, { 'r', " .-. " }, { 's', " ... " }, { 't', " - " },
                    { 'u', " ..- " }, { 'v', " ...- " }, { 'w', " .-- " }, { 'x', " -..- " },
                    { 'y', " -.-- " }, { 'z', " --.. " },
                    { '0', " ----- " }, { '1', " .---- " }, { '2', " ..--- " }, { '3', " ...-- " },
                    { '4', " ....- " }, { '5', " ..... " }, { '6', " -.... " }, { '7', " --... " },
                    { '8', " ---.. " }, { '9', " ----. " }, {' ', "|"}
                };
    
             private readonly Dictionary<string, char> alphabet_code = new Dictionary<string, char>
               {
                    { ".-", 'A' }, { "-...", 'B' }, { "-.-.", 'C' }, { "-..", 'D' },
                    { ".", 'E' }, { "..-.", 'F' }, { "--.", 'G' }, { "....", 'H' },
                    { "..", 'I' }, { ".---", 'J' }, { "-.-", 'K' }, { ".-..", 'L' },
                    { "--", 'M' }, { "-.", 'N' }, { "---", 'O' }, { ".--.", 'P' },
                    { "--.-", 'Q' }, { ".-.", 'R' }, { "...", 'S' }, { "-", 'T' },
                    { "..-", 'U' }, { "...-", 'V' }, { ".--", 'W' }, { "-..-", 'X' },
                    { "-.--", 'Y' }, { "--..", 'Z' },
                    { "-----", '0' }, { ".----", '1' }, { "..---", '2' }, { "...--", '3' },
                    { "....-", '4' }, { ".....", '5' }, { "-....", '6' }, { "--...", '7' },
                    { "---..", '8' }, { "----.", '9' }, {"|", ' '}
               };
    
            public Form1()
            {
                InitializeComponent();
               
            }
    
            private void Translate_Tomorse()
            {
                string usertext = Input.Text.ToLower();
                List<string> translated_message = new List<string>(); // morse code
    
                foreach (char letter in usertext)
                {
                    if (morse_code.ContainsKey(letter))// If the character exists in the dictionary
                    {
                        translated_message.Add(morse_code[letter]);
                    }
    
                }
                Output.Text = string.Join(" ", translated_message);
            }
    
            private void Translate_Toalphanumeric()
            {
    
                string usertext = Input.Text.ToLower();
                string[] wordsinmorse = usertext.Split('|');// Split by '|'
                List<string> Translated_phrases = new List<string>(); // alphanumeric 
    
                foreach (string word in wordsinmorse)
                {
                    string[] morse_char = word.Trim().Split(' ');// makes an array where each element is an individual Morse code character
                    List<char> decoded_char = new List<char>();//array will store the decoded characters for the current word.
    
                    foreach (string morseChar in morse_char)
                    {
                        if (alphabet_code.ContainsKey(morseChar))// If the character exists in the dictionary
                        {
                            char decodedletter = alphabet_code[morseChar];
                            decoded_char.Add(decodedletter);
                        }
                        else { decoded_char.Add('?'); }
                    }
                    Translated_phrases.Add(new string(decoded_char.ToArray()));// Convert decoded characters to a word and add to decoded words
                }
                Output.Text = string.Join(" ", Translated_phrases);
            }
    
            private void Translate_btn_Click(object sender, EventArgs e)
            {
                Translate_Toalphanumeric();
            }
    
            private void Tomorse_Click(object sender, EventArgs e)
            {
                Translate_Tomorse();
            }
        }
    }
