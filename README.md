let currentInput = '0';
let previousInput = '';
let operator = '';

keys.addEventListener('click', event => {
    const { target } = event;
    const { value } = target;

    if (!target.matches('button')) {
        return;
    }

    switch (value) {
        case '+':
        case '-':
        case '*':
        case '/':
            handleOperator(value);
            break;
        case '=':
            calculate();
            break;
        case 'all-clear':
            clearAll();
            break;
        case '.':
            inputDecimal();
            break;
        default:
            inputNumber(value);
            break;
    }
    updateScreen();
});

function handleOperator(nextOperator) {
    const inputValue = parseFloat(currentInput);

    if (operator && previousInput) {
        calculate();
    } else {
        previousInput = inputValue;
    }

    operator = nextOperator;
    currentInput = '0';
}

function calculate() {
    let result = 0;
    const previous = parseFloat(previousInput);
    const current = parseFloat(currentInput);

    if (isNaN(previous) || isNaN(current)) {
        return;
    }

    switch (operator) {
        case '+':
            result = previous + current;
            break;
        case '-':
            result = previous - current;
            break;
        case '*':
            result = previous * current;
            break;
        case '/':
            result = previous / current;
            break;
        default:
            return;
    }

    currentInput = `${result}`;
    operator = '';
    previousInput = '';
}

function clearAll() {
    currentInput = '0';
    previousInput = '';
    operator = '';
}

function inputDecimal() {
    if (!currentInput.includes('.')) {
        currentInput += '.';
    }
}

function inputNumber(number) {
    if (currentInput === '0') {
        currentInput = number;
    } else {
        currentInput += number;
    }
}

function updateScreen() {
    calculatorScreen.value = currentInput;
}
