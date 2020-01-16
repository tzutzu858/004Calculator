# 004Calculator
練習TableLayout兩個重點<br />
1.stretchColumns="*" 表示所有列都要自動拉伸<br />
2.layout_span=" " 指定該單元佔據的列数<br /><br />
<img src="https://github.com/tzutzu858/ChallengeDailyUI/blob/master/Day01_10/04_Calculator/Calculator.gif" width="300" >
<br /><br /><br />
## 主程式
```js
result =findViewById(R.id.result);
        newNumber =findViewById(R.id.operation);
        displayOperation =findViewById(R.id.textView);
        Button allClear = findViewById(R.id.allClear);
        Button button0 = findViewById(R.id.button0);
        Button button1 = findViewById(R.id.button1);
        Button button2 = findViewById(R.id.button2);
        Button button3 = findViewById(R.id.button3);
        Button button4 = findViewById(R.id.button4);
        Button button5 = findViewById(R.id.button5);
        Button button6 = findViewById(R.id.button6);
        Button button7 = findViewById(R.id.button7);
        Button button8 = findViewById(R.id.button8);
        Button button9 = findViewById(R.id.button9);
        Button buttonDot = findViewById(R.id.buttonDot);

        Button buttonEquals = findViewById(R.id.buttonEquals);
        Button buttonDivide = findViewById(R.id.buttonDivide);
        Button buttonMultiply = findViewById(R.id.buttonMultiply);
        Button buttonMinus = findViewById(R.id.buttonMinus);
        Button buttonPlus = findViewById(R.id.buttonPlus);

        //設監聽事件套在每一個數字button上
        View.OnClickListener listener = new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Button b = (Button) view;
                newNumber.append(b.getText().toString());
            }
        };

        button0.setOnClickListener(listener);
        button1.setOnClickListener(listener);
        button2.setOnClickListener(listener);
        button3.setOnClickListener(listener);
        button4.setOnClickListener(listener);
        button5.setOnClickListener(listener);
        button6.setOnClickListener(listener);
        button7.setOnClickListener(listener);
        button8.setOnClickListener(listener);
        button9.setOnClickListener(listener);
        buttonDot.setOnClickListener(listener);

        //設監聽事件套在加減乘除等於button上
        View.OnClickListener opListener = new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Button b = (Button) view;
                String op = b.getText().toString();
                String value = newNumber.getText().toString();
                if (value.length() != 0) {
                    performOperation(value, op);
                }
                pendingOperation = op;
                displayOperation.setText(pendingOperation);
            }
        };

        buttonEquals.setOnClickListener(opListener);
        buttonDivide.setOnClickListener(opListener);
        buttonMultiply.setOnClickListener(opListener);
        buttonMinus.setOnClickListener(opListener);
        buttonPlus.setOnClickListener(opListener);

        //AC鍵設定
        allClear.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                result.setText("");
                newNumber.setText("");
                displayOperation.setText("");
                operand1 = 0.0;
                operand2 = 0.0;

            }
        });




    }

    private void performOperation(String value, String operation) {
        if (null == operand1)
        {operand1 = Double.valueOf(value);}
        else
        {
            operand2 = Double.valueOf(value);

            if(pendingOperation.equals("="))
            {pendingOperation = operation;}

            switch (pendingOperation)
            {
                case "=":
                    operand1 = operand2;
                    break;
                case "/":
                    if (operand2 == 0) {
                        operand1 = 0.0;
                    } else {
                        operand1 /= operand2;
                    }
                    break;
                case "*":
                    operand1 *= operand2;
                    break;
                case "-":
                    operand1 -= operand2;
                    break;
                case "+":
                    operand1 += operand2;
                    break;
            }
        }

        result.setText(operand1.toString());
        newNumber.setText("");
```
