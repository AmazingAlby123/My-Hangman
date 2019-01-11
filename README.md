import java.util.Scanner;
import java.util.Random;

public class Hangman51{
 public static void main (String[] args) throws Exception{
  
 Scanner kb = new Scanner(System.in);
 Random rng = new Random(); 
 int r = rng.nextInt(5);
 boolean checkW = true;
 String misses = "";
 int missCounter = 1;

 
 
 String[] words = {"fruit","reading","festival","automation","window"};
 String[] wordMemmory = new String[words[r].length()];
 
 System.out.println("\nWelcome to Hangman, you will have to guess a word. \nIf you guess wrong for 5 times, you lose!\n");
 Thread.sleep(4000);
 System.out.println("-=-=-=-=-=-=-=-=-=-=-=-=-=-=-");
 System.out.print("word: ");
  for (int i = 0 ; i < words[r].length() ; i++){ //This for loop prints a underscore for each letter of the random word
   System.out.print("_ ");
   wordMemmory[i] = "_";
  }
   System.out.println("");
   System.out.println("   ____________");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("   | ");
   System.out.println("___|___");
 System.out.println("\n\nMisses: ");
 
 //Here begins de loop where you can start guessing. 
 
  do{
   System.out.print("\nGuess: ");
   String guess = kb.next();
   
   System.out.println("-=-=-=-=-=-=-=-=-=-=-=-=-=-=-");
   System.out.print("word: ");
    
    for (int i = 0 ; i < words[r].length(); i++){ // this for loop, grabs one letter of the random word at a time, changes it from a char to a string and then checks if the guess is the same as every letter from the word.

    char c = words[r].charAt(i);
    String d = String.valueOf(c);
      
     if(guess.equals(d)){
      wordMemmory[i] = guess; //if a letter matches the guess, the corrosoponding underscore in the wordMemmory array is changed to the guessed letter. 
     }
    }
    
    for(int i = 0 ; i < words[r].length() ; i++){ //This loop prints the wordMemmory array.
     System.out.print(wordMemmory[i] + " ");  
    }
    
   checkW = checkWin(wordMemmory,words,r); //checkW gets the value true or false, from the function checkWin
   boolean checkF = checkFail(wordMemmory,words,r,guess); 

  if (missCounter == 1) {
   System.out.println("\n  ____________");
   System.out.println("   |          _|_");
   System.out.println("   |         /   \\");
   System.out.println("   |        |     |");
   System.out.println("   |         \\_ _/");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("   |");
   System.out.println("___|___");
  }
  if (missCounter == 2) {
   System.out.println("\n  ____________");
   System.out.println("   |          _|_");
   System.out.println("   |         /   \\");
   System.out.println("   |        |     |");
   System.out.println("   |         \\_ _/");
   System.out.println("   |           |");
   System.out.println("   |           |");
   System.out.println("   |");
   System.out.println("___|___");
  }
  if (missCounter == 3) {
   System.out.println("\n  ____________");
   System.out.println("   |          _|_");
   System.out.println("   |         /   \\");
   System.out.println("   |        |     |");
   System.out.println("   |         \\_ _/");
   System.out.println("   |           |");
   System.out.println("   |           |");
   System.out.println("   |          / \\ ");
   System.out.println("___|___      /   \\");
  }
  if (missCounter == 4) {
   System.out.println("\n ____________");
   System.out.println("   |          _|_");
   System.out.println("   |         /   \\");
   System.out.println("   |        |     |");
   System.out.println("   |         \\_ _/");
   System.out.println("   |          _|_");
   System.out.println("   |         / | \\");
   System.out.println("   |          / \\ ");
   System.out.println("___|___      /   \\");
   }
  if (missCounter == 5) {
   System.out.println("\n\nGAME OVER!");
  System.out.println("\n  ____________");
   System.out.println("   |          _|_");
   System.out.println("   |         /x  x\\");
   System.out.println("   |        |     |");
   System.out.println("   |         \\_- _/");
   System.out.println("   |          _|_");
   System.out.println("   |         / | \\");
   System.out.println("   |          / \\ ");
   System.out.println("___|___      /   \\");
   System.out.println("GAME OVER! The word was ");
  }
   
    if(checkF == false){ //if checkF is false, the guess will be added to the variable "misses" and the missCounter will go up by one. 
     misses = misses + guess + " ";
     missCounter++;
    }
   System.out.println("\n\nMisses: " + misses);
   
    if(missCounter == 5){ //once you get 5 guesses wrong, checkW will become false and make the code leave the while loop.
     checkW = false;
    }
  }
  while(checkW == true);
 
   if(missCounter == 5){
    System.out.println("\nYou have guessed wrong 5 times, you lose!");
   }
   else{
    System.out.println("\nYou win! You're the best! "); 
   } 
  }
  
  // main closer

  public static boolean checkWin(String[] wordMemmory , String[] words, int r){ //This function checks if every letter of the random word is guessed or not
     for(int i = 0 ; i < words[r].length() ; i++){
      if (wordMemmory[i].equals("_")){
       return true; // when one of the letters is still a underscore, checkWin will return true.
      }
     }
     return false; //when the for loop does not return true, meaning there are no more underscores, it will return false here. Meaning the word is guessed.
  }
  
  public static boolean checkFail(String[] wordMemmory , String[] words, int r, String guess){ //This Function checks if a letter of the random word is guessed or not.
         
     for(int i = 0 ; i < words[r].length() ; i++){
     
     char c = words[r].charAt(i); //I only know the charAt function, so i had to convert the char to a string. 
     String d = String.valueOf(c); //Which happens in these two lines.
     
      if (d.equals(guess)){ //If one of the letters of the random word equals the guess, the function checkFail returns true. Meaning you did not guess wrong.
       return true;
      }
     }
     return false; //when the for loop does not return true, meaning you did not guess right, it will return false here. Meaning the guessed letter is wrong. 
  }

} // class closer
