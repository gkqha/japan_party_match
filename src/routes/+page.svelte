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
        "13": 5,
        "14": 3,
        "15": 5,
        "16": 1,
        "17": 4,
        "18": 3,
        "19": 2,
        "20": 3,
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
            "13": 5,
            "14": 1,
            "15": 2,
            "16": 1,
            "17": 3,
            "18": 3,
            "19": 3,
            "20": 3,
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
            "13": 5,
            "14": 1,
            "15": 1,
            "16": 3,
            "17": 4,
            "18": 4,
            "19": 3,
            "20": 4,
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
            "13": 1,
            "14": 1,
            "15": 1,
            "16": 2,
            "17": 1,
            "18": 4,
            "19": 3,
            "20": 3,
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
            "13": 5,
            "14": 1,
            "15": 1,
            "16": 2,
            "17": 5,
            "18": 5,
            "19": 2,
            "20": 5,
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
            "13": 2,
            "14": 2,
            "15": 2,
            "16": 3,
            "17": 2,
            "18": 3,
            "19": 2,
            "20": 3,
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
            "13": 5,
            "14": 1,
            "15": 1,
            "16": 1,
            "17": 5,
            "18": 5,
            "19": 1,
            "20": 3,
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
            "13": 5,
            "14": 1,
            "15": 1,
            "16": 3,
            "17": 5,
            "18": 5,
            "19": 2,
            "20": 5,
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
            "13": 3,
            "14": 5,
            "15": 1,
            "16": 3,
            "17": 5,
            "18": 4,
            "19": 1,
            "20": 3,
        },
    ]
    const partyName = ["自由民主党", "公明党", "立宪民主党", "日本维新会", "日本共产党", "国民民主党", "令和新选组", "社会民主党", "参政党"]
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
        "问题13：养老金应和自己的收入挂钩",
        "问题14：夫妻可以不同姓",
        "问题15：禁止企业团体向政党捐款",
        "问题16：设置专门的防灾部门",
        "问题17：拼车合法化",
        "问题18：为了治安应牺牲个人权利",
        "问题19：通过公共事业来保障就业",
        "问题20：提高经济竞争力比社会平等更重要",
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
<style>
    /* General Styling */
    body {
        font-family: sans-serif;
        line-height: 1.6;
        margin: 20px;
        background-color: #f4f4f4;
        color: #333;
    }

    h2 {
        color: #2c3e50;
        margin-bottom: 10px;
    }

    p {
        margin-bottom: 15px;
    }

    label {
        display: block;
        margin-bottom: 10px;
        cursor: pointer;
    }

    input[type="radio"] {
        margin-right: 5px;
    }


    /* Button Styling */
    button {
        background-color: #4CAF50;
        border: none;
        color: white;
        padding: 10px 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin: 4px 2px;
        cursor: pointer;
        border-radius: 5px;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #45a049;
    }

    button:disabled {
        background-color: #ddd;
        color: #999;
        cursor: default;
    }

    /* Container for question and options */
    .question-container {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        margin-bottom: 20px;
    }

    


</style>

{#if questions.length > 0 && currentQuestion < questions.length}
    <div class="question-container">
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
    </div>
{:else if questions.length > 0}
    <button on:click={submitAnswers}>提交答案</button>
{:else}
    <p>Loading...</p>
{/if}