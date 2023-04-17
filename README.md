private static final String[] romanNumerals = {"I", "IV", "V", "IX", "X", "XL", "L", "XC", "C"};
private static final int[] romanValues = {1, 4, 5, 9, 10, 40, 50, 90, 100};

public static String calc(String input) throws IllegalArgumentException {
    String[] inputs = input.split(" ");
    validateInput(inputs);
    int num1, num2;
    try {
        num1 = Integer.parseInt(inputs[0]);
        num2 = Integer.parseInt(inputs[2]);
    } catch (NumberFormatException e) {
        num1 = romanToArabic(inputs[0]);
        num2 = romanToArabic(inputs[2]);
    }
    int result = perform(operationCharToCode(inputs[1]), num1, num2);
    return formatResult(result, inputs[0], inputs[2]);
}

private static void validateInput(String[] inputs) throws IllegalArgumentException {
    if (inputs.length != 3) {
        throw new IllegalArgumentException("Invalid input format");
    }
    char operation = inputs[1].charAt(0);
    if (operation != '+' && operation != '-' && operation != '*' && operation != '/') {
        throw new IllegalArgumentException("Unsupported operation");
    }
    boolean isArabic = isNumber(inputs[0]) && isNumber(inputs[2]);
    boolean isRoman = !isArabic && isRomanNumeral(inputs[0]) && isRomanNumeral(inputs[2]);
    if (!isArabic && !isRoman) {
        throw new IllegalArgumentException("Mixed numerals are not supported");
    }
}

private static boolean isNumber(String str) {
    try {
        Integer.parseInt(str);
        return true;
    } catch (NumberFormatException e) {
        return false;
    }
}

private static boolean isRomanNumeral(String str) {
    for (char c : str.toCharArray()) {
        if (c != 'I' && c != 'V' && c != 'X' && c != 'L' && c != 'C') {
            return false;
        }
    }
    return true;
}

private static int romanToArabic(String str) throws IllegalArgumentException {
    int result = 0;
    String lastTwoChars = "";
    for (int i = str.length() - 1; i >= 0; i--) {
        String twoChars = "";
        if (i > 0) {
            twoChars = str.substring(i - 1, i + 1);
        }
        if (lastTwoChars.equals(twoChars)) {
            throw new IllegalArgumentException("Invalid Roman numeral");
        }
        lastTwoChars = twoChars;
        int value = romanCharToValue(str.charAt(i));
        if (i == str.length() - 1 || value >= romanCharToValue(str.charAt(i + 1))) {
            result += value;
        } else {
            result -= value;
        }
    }
    return result;
}

private static int romanCharToValue(char c) throws IllegalArgumentException {
    for (int i = romanNumerals.length - 1; i >= 0; i--) {
        if (c == romanNumerals[i].charAt(0) || c == romanNumerals[i].charAt(1)) {
            return romanValues[i];
        }
    }
    throw new IllegalArgumentException("Invalid Roman numeral");
}

private static int operationCharToCode(String str) {
    char op = str.charAt(0);
    if (op == '+') {
        return 0;
    } else if (op == '-') {
        return 1;
    } else if (op == '*') {
        return 2;
    } else {
        return 3;
    }
}

private static int perform(int code, int num1, int num2) {
    if (code == 0) {
        return num1 + num2;
    } else if (code == 1) {
        return num1 - num2;
    } else if (code == 2) {
        return num1 * num2;
    } else {
        return num1 / num2;
    }
}

private static String formatResult(int result, String num1Str, String num2Str) {
    if (isNumber(num1Str) && isNumber(num2Str)) {
        return String.valueOf(result);
    } else {
        return arabicToRoman(result);
    }
}

private static String arabicToRoman(int num) throws IllegalArgumentException {
    if (num <= 0) {
        throw new IllegalArgumentException("Roman numerals can only be positive");
    }
    StringBuilder sb = new StringBuilder();
    int remainder = num;
    for (int i = romanValues.length - 1; i >= 0; i--) 
    }   
