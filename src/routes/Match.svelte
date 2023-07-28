<script>
    const getNewQuestion = () => [ Math.ceil(Math.random() * 10), Math.ceil(Math.random() * 10) ]
    const questionArray = Array.from({ length: 5 }, () => getNewQuestion())
    const answerArray = questionArray.map(question => question[0] * question[1])

    const getRandomAnswer = () => {
        const randomIndex = Math.floor(Math.random() * answerArray.length)
        const randomAnswer = answerArray[randomIndex]
        answerArray.splice(randomIndex, 1)
        return randomAnswer
    }

    let selectedButtons = []

    const handleButtonClick = ({ target }) => {
        const button = target
        button.classList.toggle('selected')

        // If the button is already selected, remove it from the selectedButtons.
        if (selectedButtons.includes(button)) {
            selectedButtons = selectedButtons.filter(currentButton => currentButton !== button)
            return
        }

        // TODO: Untoggle buttons as appropriate.
        
        // If button is question and selectedButtons already contains a question, replace the selectedButtons with the new question; or
        // if button is answer and selectedButtons already contains an answer, replace the selectedButtons with the new answer.
        // Otherwise, add the button to the selectedButtons.
        if (
            selectedButtons.filter(currentButton => currentButton.classList.contains('question')).length === 1 && button.classList.contains('question') ||
            selectedButtons.filter(currentButton => currentButton.classList.contains('answer')).length === 1 && button.classList.contains('answer')
        ) {
            selectedButtons = [ button ]
            return
        }
        
        selectedButtons = [ ...selectedButtons, button ]

        if (selectedButtons.length === 2) {
            const question = selectedButtons.filter(currentButton => currentButton.classList.contains('question'))[0].textContent.split(' x ').map(number => parseInt(number)).reduce((a, b) => a * b)
            const answer = parseInt(selectedButtons.filter(currentButton => currentButton.classList.contains('answer'))[0].textContent)
            if (question === answer) {
                console.log('correct')
            } else {
                console.log('incorrect')
            }
            selectedButtons.forEach(button => button.classList.remove('selected')
            selectedButtons = []
        }
    }
</script>

{#each questionArray as question}
    <div>
        <button class='question' on:click={handleButtonClick}>
            {question[0]} x {question[1]}
        </button>
        <button class='answer' on:click={handleButtonClick}>
            {getRandomAnswer()}
        </button>
    </div>
{/each}

<style>
    button {
        font-size: 2rem;
        font-weight: bold;
        color: var(--text-color);
        background-color: var(--primary-color);
        width: 150px;
        margin: 10px;
        padding: 12px 16px;
        cursor: pointer;
        border-radius: 16px;
        border: 2px solid var(--text-color);
        border-bottom: 6px solid var(--text-color);
        transition: all 0.1s;
    }

    button:hover {
        background-color: var(--secondary-color);
    }

    button:active {
        background-color: var(--tertiary-color);
        border-bottom: 2px solid var(--text-color);
    }

    .selected {
        background-color: var(--tertiary-color);
        border-bottom: 2px solid var(--text-color);
    } 
</style>