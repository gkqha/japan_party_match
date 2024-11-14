<script>
    let answers = {};
    const options = ['非常同意', '同意', '中立', '反对', '非常反对'];
    const data = [{
        "1": 3,
        "2": 3,
        "3": 5,
        "4": 3,
        "5": 3,
        "6": 1,
        "7": 3,
        "8": 4,
        "9": 3,
        "10": 1,
        "11": 2,
        "12": 4,
    },
        {
            "1": 3,
            "2": 2,
            "3": 4,
            "4": 3,
            "5": 2,
            "6": 1,
            "7": 3,
            "8": 4,
            "9": 3,
            "10": 2,
            "11": 2,
            "12": 2,
        },
        {
            "1": 2,
            "2": 2,
            "3": 5,
            "4": 4,
            "5": 3,
            "6": 1,
            "7": 3,
            "8": 1,
            "9": 5,
            "10": 5,
            "11": 1,
            "12": 1,
        },
        {
            "1": 5,
            "2": 1,
            "3": 1,
            "4": 1,
            "5": 3,
            "6": 1,
            "7": 5,
            "8": 2,
            "9": 1,
            "10": 1,
            "11": 1,
            "12": 1,
        },
        {
            "1": 1,
            "2": 1,
            "3": 1,
            "4": 5,
            "5": 3,
            "6": 1,
            "7": 1,
            "8": 1,
            "9": 5,
            "10": 5,
            "11": 5,
            "12": 1,
        },
        {
            "1": 5,
            "2": 1,
            "3": 1,
            "4": 2,
            "5": 2,
            "6": 1,
            "7": 4,
            "8": 1,
            "9": 1,
            "10": 2,
            "11": 2,
            "12": 3,
        },
        {
            "1": 1,
            "2": 3,
            "3": 1,
            "4": 5,
            "5": 3,
            "6": 1,
            "7": 5,
            "8": 1,
            "9": 5,
            "10": 5,
            "11": 3,
            "12": 1,
        },
        {
            "1": 1,
            "2": 1,
            "3": 1,
            "4": 5,
            "5": 3,
            "6": 1,
            "7": 3,
            "8": 1,
            "9": 5,
            "10": 5,
            "11": 1,
            "12": 1,
        },
        {
            "1": 3,
            "2": 5,
            "3": 1,
            "4": 2,
            "5": 3,
            "6": 2,
            "7": 5,
            "8": 1,
            "9": 2,
            "10": 5,
            "11": 1,
            "12": 5,
        },
        {
            "1": 4,
            "2": 1,
            "3": 1,
            "4": 3,
            "5": 2,
            "6": 1,
            "7": 4,
            "8": 2,
            "9": 5,
            "10": 1,
            "11": 1,
            "12": 3,
        },
    ]
    const partyName = ["自由民主党", "公明党", "立宪民主党", "日本维新会", "日本共产党", "国民民主党", "令和新选组", "社会民主党", "参政党", "与大家一起创造党"]
    // 定义问题内容的数组
    const questions = [
        "问题1：对大公司增加税收",
        "问题2：对高收入人群收取更高的税",
        "问题3：降低消费税",
        "问题4：增加老年人医疗的自付比例",
        "问题5：国家财政更关心少子化而不是老龄化",
        "问题6：大学免学费",
        "问题7：物价上涨不能超过2%",
        "问题8：对农民收入进行补偿",
        "问题9：增设新核电站",
        "问题10：社保卡、驾照等整合入身份证",
        "问题11：国家机关驻地分散各省",
        "问题12：同性婚姻合法化",
    ];


    let currentQuestion = 0; // 从0开始，方便数组索引


    function prevQuestion() {
        if (currentQuestion > 1) {
            currentQuestion--;
        }
    }

    function euclideanDistance(json1, json2) {
        let sumOfSquares = 0;
        for (let key in json1) {
            sumOfSquares += Math.pow(json1[key] - json2[key], 2);
        }
        return Math.sqrt(sumOfSquares);
    }

    function nextQuestion() {
        if (answers[currentQuestion + 1] !== undefined) { // 检查当前问题是否已回答
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
            }
        } else {
            alert(`请回答问题 ${currentQuestion + 1}`); // 提示用户回答当前问题
        }
    }

    function handleAnswerSelect(question, answer) {
        answers[question] = options.indexOf(answer) + 1; // 将选项转换为对应的数字
    }

    function submitAnswers() {
        const answeredOptions = {}; // 创建一个新的对象来存储答案
        for (const key in answers) {
            answeredOptions[key] = answers[key];
        }
        const json = JSON.stringify(answeredOptions, null, 2);
        console.log(json);
        const partyMatchIndex = [];
        for (const item of data) {
            partyMatchIndex.push(euclideanDistance(answeredOptions, item))
        }

        function findIndexOfMin(arr) {
            if (arr.length === 0) {
                return -1; // 处理空数组的情况
            }

            return arr.reduce((minIndex, currentValue, currentIndex, array) => {
                return currentValue < array[minIndex] ? currentIndex : minIndex;
            }, 0); // 初始的 minIndex 为 0
        }

        const partyMatch = partyName[findIndexOfMin(partyMatchIndex)];
        alert(partyMatch);
    }


</script>
{#if questions.length > 0 && currentQuestion < questions.length}
    <h2>{questions[currentQuestion]}</h2>
    <p>请选择一个选项:</p>
    {#each options as option, index}
        <label>
            <input
                    type="radio"
                    name="question-{currentQuestion + 1}"
                    value={option}
                    on:change={() => handleAnswerSelect(currentQuestion + 1, option)}
                    checked={answers[currentQuestion + 1] === index + 1}
            >
            {option}
        </label><br>
    {/each}
    <button on:click={prevQuestion} disabled={currentQuestion === 0}>上一题</button>
    {#if currentQuestion < questions.length - 1}
        <button on:click={nextQuestion} disabled={answers[currentQuestion + 1] === undefined}>下一题</button>
    {:else}
        <button on:click={submitAnswers}>提交答案</button>
    {/if}

{:else if questions.length > 0}
    <button on:click={submitAnswers}>提交答案</button>
{:else}
    <p>Loading...</p>
{/if}