package com.robatortas.Calculator;

//imports

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Calculator implements ActionListener{

    //button assignment

    JFrame frame;
    JTextField textField;
    JTextField version;
    JButton[] numberButtons = new JButton[10];
    JButton[] functionButtons = new JButton[9];
    JButton addButton,subButton,mulButton,divButton;
    JButton decButton, equButton, delButton, clrButton, negButton;
    JPanel panel;
    JLabel label = new JLabel();

    //font

    Font myFont = new Font("Agency FB", Font.BOLD,30);
    Font resultText = new Font("Agency FB", Font.BOLD,35);
    Font versionText = new Font("Arial", Font.PLAIN, 10);

    //settings

    double num1=0,num2=0,result=0;
    char operator;

    Calculator(){

        //frame

        frame = new JFrame("Calculator Java Edition ALPHA 1.1.0.0");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(320, 472);
        frame.setResizable(false);
        frame.setLayout(null);

        //text

        textField = new JTextField();
        textField.setFont(resultText);
        textField.setForeground(Color.white);
        textField.setHorizontalAlignment(SwingConstants.RIGHT);
        textField.setEditable(false);
        textField.setFocusable(false);
        textField.setBackground(Color.darkGray);
        textField.setBorder(null);

        version = new JTextField();
        version.setText("ALPHA 1.1.0.0");
        version.setFont(versionText);
        version.setForeground(Color.white);
        version.setEditable(false);
        version.setFocusable(false);
        version.setBackground(Color.darkGray);
        version.setBorder(null);


        //CUSTOM COLOR

        Color customColor = new Color(155, 155, 191);
        Color customColor2 = new Color(212, 121, 2);

        //Symbols

        addButton = new JButton("+");
        subButton = new JButton("-");
        mulButton = new JButton("*");
        divButton = new JButton("/");
        decButton = new JButton(".");
        equButton = new JButton("=");
        delButton = new JButton("<--");
        clrButton = new JButton("Clear");
        negButton = new JButton("(-)");

        //function buttons

        functionButtons[0] = addButton;
        functionButtons[1] = subButton;
        functionButtons[2] = mulButton;
        functionButtons[3] = divButton;
        functionButtons[4] = decButton;
        functionButtons[5] = equButton;
        functionButtons[6] = delButton;
        functionButtons[7] = clrButton;
        functionButtons[8] = negButton;

        //group for buttons (for loop) GUI

        for(int i =0;i<9;i++){
            functionButtons[i].addActionListener(this);
            functionButtons[i].setFont(myFont);
            functionButtons[i].setFocusable(false);
            functionButtons[i].setBackground(customColor2);
            functionButtons[i].setBorderPainted(false);
            functionButtons[i].setContentAreaFilled(true);
        }

        for(int i =0;i<10;i++){
            numberButtons[i] = new JButton(String.valueOf(i));
            numberButtons[i].addActionListener(this);
            numberButtons[i].setFont(myFont);
            numberButtons[i].setFocusable(false);
            numberButtons[i].setBackground(Color.GRAY);
            numberButtons[i].setBorderPainted(false);
            numberButtons[i].setContentAreaFilled(true);
        }

        //Bounds

        negButton.setBounds(3, 371, 98, 60);
        delButton.setBounds(103,371, 98, 60);
        clrButton.setBounds(203, 371, 98, 60);
        textField.setBounds(3, 15, 300, 50);
        version.setBounds(3, 0, 100, 20);

        panel = new JPanel();
        panel.setBounds(50, 100, 300, 300);
        panel.setLayout(new GridLayout(4, 4, 2, 2));

        //panel

        panel.add(numberButtons[1]);
        panel.add(numberButtons[2]);
        panel.add(numberButtons[3]);
        panel.add(addButton);
        panel.add(numberButtons[4]);
        panel.add(numberButtons[5]);
        panel.add(numberButtons[6]);
        panel.add(subButton);
        panel.add(numberButtons[7]);
        panel.add(numberButtons[8]);
        panel.add(numberButtons[9]);
        panel.add(mulButton);
        panel.add(decButton);
        panel.add(numberButtons[0]);
        panel.add(equButton);
        panel.add(divButton);

        //panel Costumization

        panel.setBackground(Color.darkGray);
        panel.setLocation(2, 70);

        //frame

        frame.add(panel);
        frame.add(negButton);
        frame.add(delButton);
        frame.add(clrButton);;
        frame.add(textField);
        frame.add(version);
        frame.setVisible(true);
        frame.getContentPane().setBackground(Color.darkGray);
        frame.setLocationRelativeTo(null);
        frame.setResizable(false);

    }

    public static void main(String[] args) {

        Calculator calc = new Calculator();
    }

    //Action Listener

    @Override
    public void actionPerformed(ActionEvent e) {

        //for loop numberButtons

        for(int i=0;i<10;i++) {
            if(e.getSource() == numberButtons[i]) {
                textField.setText(textField.getText().concat(String.valueOf(i)));
            }
        }

        //if statements (a lot of them)

        if (e.getSource() == decButton) {
            textField.setText(textField.getText().concat("."));
        }
        if (e.getSource() == addButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '+';
            textField.setText("");
        }
        if (e.getSource() == subButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '-';
            textField.setText("");
        }
        if (e.getSource() == mulButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '*';
            textField.setText("");
        }
        if (e.getSource() == divButton) {
            num1 = Double.parseDouble(textField.getText());
            operator = '/';
            textField.setText("");
        }
        if (e.getSource() == clrButton) {
            textField.setText("");
        }
        if (e.getSource() == delButton) {
            String delete = textField.getText();
            textField.setText("");
            for (int i = 0; i < delete.length() - 1; i++) {
                textField.setText(textField.getText() + delete.charAt(i));
            }
        }
            if (e.getSource() == negButton) {
                double temp = Double.parseDouble(textField.getText());
                temp*=-1;
                textField.setText(String.valueOf(temp));
                }

            //Equal Button (results)

        if (e.getSource() == equButton) {
            num2 = Double.parseDouble(textField.getText());
            switch(operator) {
                case'+':
                    result = num1+num2;
                    break;
                case'-':
                    result = num1-num2;
                    break;
                case'*':
                    result = num1*num2;
                    break;
                case'/':
                    result = num1/num2;
                    break;
            }
            textField.setText(String.valueOf(result));

            }

        }
    }