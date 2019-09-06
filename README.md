# How to automatically open your Jupyter Notebook (.ipynb) file with a double click?
Have you ever experienced the hassle of opening an Jupyter Notebook (.ipynb) file? If you've worked with Jupyter Notebooks before you've probably had. To ease the hassle, I have created an **Automator AppleScript that will open your ipynb file directly as a Jupyter Notebook in your browser.** The solution presented however is only compatible with Mac OS.


## Two usual ways of opening an ipynb file
  1. Opening in the Jupyter Notebook Environment
  
      ![jupyter](visuals/jupyter.gif "jupyter")

  2. Opening through the terminal by entering:
      
      ```jupyter notebook ~/filepath/filename.ipynb```
      
      ![terminal_open](visuals/terminal_open.gif "terminal_open")

     Note that you have to be in the directory of the file to open the Jupyter Notebook.
     
      ![wrong_directory](visuals/wrong_directory.gif "wrong_directory")

## Your step by step guide to open your Jupyter Notebook (.ipynb) file with a double click
The solution created was based on the second method mentioned above and ghoppe's answer in https://superuser.com/questions/139352/mac-os-x-how-to-open-vim-in-terminal-when-double-click-on-a-file. Below are the detailed steps for the automator solution.
  1. Open "Automator.app" from your Finder
  
      ![step1](visuals/step1.png "step1")
      
  2. Create a "New Document"
  
      ![step2](visuals/step2.png "step2")
      
  3. Choose "Application"
  
      ![step3](visuals/step3.png "step3")

  4. Find and select "Run AppleScript"
  
      ![step4](visuals/step4.png "step4")

  5. Paste the code in the AppleScript
  
      ![step5](visuals/step5.png "step5")

    ```
    on run {input}
       set the_path to POSIX path of input
       set cmd to "jupyter notebook " & quoted form of the_path
       tell application "System Events" to set terminalIsRunning to exists application process "Terminal"
       tell application "Terminal"
          activate
          if terminalIsRunning is true then
             do script with command cmd
          else
             do script with command cmd in window 1
          end if
       end tell
    end run
    ```

  6. Save as "automatic_ipynb_opener.app" or any desired name for your app
  
      ![step6](visuals/step6.png "step6")

  7. Go to any .ipynb file, open "Get Info" and select "Other..." under "Open with"
  
      ![step7](visuals/step7.png "step7")
      
      ![step7.2](visuals/step7.2.png "step7.2")

  8. Find and select your app and tick "Always Open With"
  
      ![step8](visuals/step8.png "step8")

  9. Click "Change All..."
  
      ![step9](visuals/step9.png "step9")

  10. Check and confirm the automator by double-clicking your .ipynb file
  
      ![automator](visuals/automator.gif "automator")

That's it! You now have an Automator AppleScript that will open your ipynb file directly as a Jupyter Notebook in your browser. You are now saved from seconds, minutes, or even hours of non-value adding activity. Enjoy!

## Reference: 

https://superuser.com/questions/139352/mac-os-x-how-to-open-vim-in-terminal-when-double-click-on-a-file

