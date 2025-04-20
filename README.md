

package com.example.javanotesmanager;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class javanotesmanager {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        
        System.out.println("Enter text for JavaFile1.txt:");
        String text1 = scanner.nextLine();
        createNote("JavaFile1.txt", text1);

       
        System.out.println("Content of JavaFile1.txt:");
        displayNote("JavaFile1.txt");

      
        System.out.println("Enter text for JavaFile2.txt:");
        String text2 = scanner.nextLine();
        createNote("JavaFile2.txt", text2);

        
        copyNoteContent("JavaFile1.txt", "JavaFile2.txt");

        
        analyzeNote("JavaFile1.txt");

     
        searchWordInNote("JavaFile1.txt", "polymorphism");

        scanner.close();
    }

    private static void createNote(String filename, String text) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
            writer.write(text);
            System.out.println("Note created successfully.");
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }

    private static void displayNote(String filename) {
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }

    private static void copyNoteContent(String srcFilename, String destFilename) {
        try (BufferedReader reader = new BufferedReader(new FileReader(srcFilename));
             BufferedWriter writer = new BufferedWriter(new FileWriter(destFilename, true))) {
            String line;
            writer.newLine(); // Add a new line before appending content
            while ((line = reader.readLine()) != null) {
                writer.write(line);
                writer.newLine();
            }
            System.out.println("Note content copied successfully.");
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }

    private static void analyzeNote(String filename) {
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            int characters = 0;
            int lines = 0;
            int words = 0;
            String line;
            while ((line = reader.readLine()) != null) {
                lines++;
                characters += line.length();
                words += line.split("\\s+").length;
            }
            System.out.println("Total characters: " + characters);
            System.out.println("Total lines: " + lines);
            System.out.println("Total words: " + words);
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }

    private static void searchWordInNote(String filename, String wordToFind) {
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            int lineNumber = 0;
            int occurrences = 0;
            String line;
            while ((line = reader.readLine()) != null) {
                lineNumber++;
                if (line.toLowerCase().contains(wordToFind.toLowerCase())) {
                    occurrences++;
                    System.out.println("Word '" + wordToFind + "' found at line " + lineNumber);
                }
            }
            System.out.println("Total occurrences of '" + wordToFind + "': " + occurrences);
        } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
        }
    }
}


