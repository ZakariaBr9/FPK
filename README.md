Le Code Javascript : 

function initialiser_calc(id) {
    const champ = document.getElementById(id + '_resultat');
    champ.value = '';
}

function add_calc(id, valeur) {
    const champ = document.getElementById(id + '_resultat');
    champ.value += valeur;
}

function f_calc(id, action) {
    const champ = document.getElementById(id + '_resultat');
    let val = champ.value;

    switch (action) {
        case 'ce':
            champ.value = '';
            break;

        case 'nbs':
            champ.value = val.slice(0, -1);
            break;

        case '+-':
            if (val.charAt(0) === '-') {
                champ.value = val.slice(1);
            } else if (val !== '') {
                champ.value = '-' + val;
            }
            break;

        case '=':
            try {
                let expression = val.replace(',', '.').replace(/÷/g, '/');
                champ.value = eval(expression);
            } catch (e) {
                champ.value = "Erreur";
            }
            break;

        default:
            champ.value += action;
            break;
    }
}

function key_detect_calc(id, event) {
    const key = event.key;

    if (!isNaN(key)) {
        add_calc(id, key);
    } else if (['+', '-', '*', '/', '%', '.'].includes(key)) {
        f_calc(id, key);
    } else if (key === 'Enter') {
        f_calc(id, '=');
    } else if (key === 'Backspace') {
        f_calc(id, 'nbs');
    } else if (key === 'Escape') {
        f_calc(id, 'ce');
    }
}
