# so1

[English](README.md) | [简体中文](README.zh.md)

Make Claude 3.5 Sonnet generate thought chains like o1!

😎 100% solves the "9.9,9.11" and 80% for "strawberry" problems:

![demo](https://github.com/user-attachments/assets/043ef6b1-11bf-4512-8297-3127aa7b7734)


🧙‍♀️ prompt:

```python
# Author: Huanshere
# Version: 0.2
# Language: en-US
# Model: Claude 3.5 Sonnet
# Purpose: Step-by-step explanation of reasoning process, output in Markdown format

def analysis_assistant():
    """You are an AI assistant skilled at explaining reasoning processes step by step"""
    return {
        "style": ["rational", "detailed", "critical thinking", "reflective examination"],
        "expertise": "multi-step reasoning",
        "output_format": "Markdown"
    }

class ReasoningAssistant(input):
    def __init__(self, input):
        self.state = "understand and analyze the problem"  # Initialize step 1
        self.input = input

    def step_by_step_reasoning(self):

        def title(state, input):
            """Generate the topic you need to reason about for this step based on the current state and input"""
            return title

        def reasoning(state, input):
            """**Conduct careful and detailed reasoning, noting your limitations as an LLM and what you can and cannot do. Use at least 3 different methods to reason. When you say you are examining, actually execute the examination process. Use best practices. Include exploration of alternative answers, carefully check where you might be wrong, and where errors might occur if the reasoning is incorrect. Fully explore all possible answers. Perform at least 5 steps of reasoning, the more detailed reasoning steps the better.**"""
            return reasoning_process

        def decide_next_step(state, input, current_step):
            """Dynamically decide the next step based on the state, input, and current step"""
            if can_conclude(state, input):
                return "conclusion"
            else:
                return "continue"

        current_step = 0
        
        md_output = "# Reasoning Chain\n"
        while self.state != "conclusion":
            current_step += 1
            next_action = decide_next_step(self.state, self.input, current_step)
            
            md_output += f"## Step {current_step}: {self.state}\n"
            md_output += f"- **Reasoning**: {reasoning(self.state, self.input)}\n"
            if next_action != "conclusion":
                md_output += f"- **Next Step**: {next_action}\n\n"
            
            self.state = next_action
        
        return md_output

def start():
    """Run at startup"""
    system_role = analysis_assistant()
    print("What's the problem?")
    input = input()
    assistant = ReasoningAssistant(input)
    result = assistant.step_by_step_reasoning()

    print(result)


if __name__ == "__main__":
    start()

# Please run according to the rules, directly execute main, print("What's the problem?"), do not attempt to explain the code.
```

Prompt Reference: [g1](https://github.com/bklieger-groq/g1)

## 🧮 Gaokao 2024 Math Test!

### Testing Method
Using FastGPT low-code workflow for quick setup, we used Gaokao Math 2024 New I paper multiple-choice questions as the test questions. Each question was independently asked 3 times to all selected LLMs, and the results were summarized. The results are for reference only and do not have strict statistical significance.

In the model names, the "+" after indicates a prompt, while the rest are unprompted APIs. ✅❌ indicates correctness or incorrectness, ⚠️ indicates no result was given, and the columns from the second one onwards represent question numbers.

### Test Results
#### Total Score 🏆
| Model | Single-choice Score | Multiple-choice Score | Total Score | Percentage |
|-------|---------------------|------------------------|-------------|------------|
| 4o | 30 | 9 | 39 | 67% |
| 4omini | 30 | 9 | 39 | 67% |
| sonnet | 30 | 12 | 42 | 72% |
| **sonnet + so1** | 35 | 10 | 45 | **77%🥉** |
| sonnet + g1 * | 30 | 5 | 35 | 60% |
| **o1 mini** | 37 | 16 | 53 | **91%🥇** |
| **o1 preview** | 38 | 12 | 50 | **86%🥈**|

> Note: sonnet+g1 tends to stop after giving only the first step of reasoning, marked as ⚠️. In scoring, it is simply counted as incorrect, but its actual performance is similar to so1.

#### Single-choice Questions
| Model | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|------|---|---|---|---|---|---|---|---|
| 4o | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅❌❌ | ✅✅✅ | ✅✅✅ | ❌✅❌ | ✅❌❌ |
| 4omini | ✅✅✅ | ✅❌✅ | ✅✅✅ | ❌✅✅ | ✅✅✅ | ✅❌✅ | ✅✅✅ | ❌❌❌ |
| sonnet | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅❌❌ | ✅✅✅ | ✅❌✅ | ✅✅✅ | ❌❌❌ |
| **sonnet + so1** | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅❌ | ✅✅✅ | ❌❌✅ |
| sonnet + g1 | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅❌✅ | ✅✅⚠️ | ⚠️✅❌ | ✅✅✅ | ❌✅❌ |
| o1 mini | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅❌❌ | ✅✅✅ | ✅✅✅ |
| o1 preview | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅✅ | ✅✅❌ | ✅✅✅ | ✅✅✅ |

#### Multiple-choice Questions
| Model | 9 | 10 | 11 |
|------|---|----|----|
| 4o | ✅✅✅ | 👍👍❌ | ❌❌👍 |
| 4omini | ✅✅✅ | ❌👍👍 | ❌❌👍 |
| sonnet | ✅✅✅ | 👍👍❌ | 👍✅👍 |
| **sonnet + so1** | ✅✅✅ | ❌❌👍 | 👍👍👍 |
| sonnet + g1 | ✅❌⚠️ | ⚠️❌✅ | ⚠️❌👍 |
| o1 mini | ✅✅✅ | ✅✅✅ | ❌✅✅ |
| o1 preview | ✅✅✅ | ✅✅✅ | ❌❌❌ |

## Summary and Reflections:

1. Model performance ranking: o1 >> sonnet + so1 ~ sonnet + g1 ~> sonnet > 4o >> 4omini

2. sonnet + g1 has stability issues, occasionally stopping after generating a single line of thought. In comparison, so1 can consistently generate logical chains, indicating that the pseudo-code prompt framework has a positive effect on generating logical chains.

3. The o1 model may have already included 2024 Gaokao content in its training set? Surprisingly, mini's performance is even better than preview...

4. sonnet + so1 responds faster than o1, but o1 provides higher quality answers.
   This might suggest that o1 employs a more complex and in-depth reasoning process.

5. sonnet sometimes outperforms sonnet + so1, indicating that sonnet itself may have already been trained on Chain of Thought (CoT) synthetic data.
   If sonnet were to be trained using the latest data similar to o1, its performance could potentially surpass o1.

6. The scoring mechanism for multiple-choice questions (partial credit for partially correct answers, no credit for over-selection) highlights the advantage of so1's reflection mechanism,
   which can effectively balance multiple options and improve the scoring rate.

### Gaokao Test Set
New I paper multiple-choice questions:
```
1、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
已知集合 $A = {x \mid -5 < x^3 < 5}$，$B = {-3, -1, 0, 2, 3}$，则 $A \cap B =$ ( )

A. ${-1, 0}$
B. ${2, 3}$
C. ${-3, -1, 0}$
D. ${-1, 0, 2}$

==========A==========

2、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
若 $\frac{z}{z - 1} = 1 + i$，则 $z =$ ( )

A. $-1 - i$
B. $-1 + i$
C. $1 - i$
D. $1 + i$

==========C==========

3、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
已知向量 $a = (0, 1)$，$b = (2, x)$，若 $b \perp (b - 4a)$，则 $x =$ ( )

A. $-2$
B. $-1$
C. $1$
D. $2$

==========D==========

4、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
已知 $\cos(\alpha + \beta) = m$，$\tan \alpha \tan \beta = 2$，则 $\cos(\alpha - \beta) =$ ( )

A. $-3m$
B. $-\frac{m}{3}$
C. $\frac{m}{3}$
D. $3m$

==========A==========

5、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
已知圆柱和圆锥的底面半径相等，侧面积相等，且它们的高均为 $\sqrt{3}$，则圆锥的体积为 ( )

A. $2\sqrt{3}\pi$
B. $3\sqrt{3}\pi$
C. $6\sqrt{3}\pi$
D. $9\sqrt{3}\pi$

==========B==========

6、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
已知函数 \( f(x) \) 定义如下：
$$
f(x) = 
\begin{cases} 
e^{-x} + \ln(x + 1), & \text{if } x \geq 0 \\
-x^2 - 2ax - a, & \text{if } x < 0 
\end{cases}
$$
如果函数在实数集 \( \mathbb{R} \) 上单调递增，则 \( a \) 的取值范围是：
A. $(-\infty, 0]$
B. $[-1, 0]$
C. $[-1, 1]$
D. $[0, +\infty)$

==========B==========

7、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
当 $x \in [0, 2\pi]$ 时，曲线 $y = \sin x$ 与 $y = 2\sin(3x - \frac{\pi}{6})$ 的交点个数为 ( )

A. $3$
B. $4$
C. $6$
D. $8$

==========C==========

8、请完成下面一道选择题，每个小题四个选项中，只有一项是符合题目要求的。
已知函数 $f(x)$ 的定义域为 $\mathbb{R}$，$f(x) > f(x - 1) + f(x - 2)$，且当 $x < 3$ 时，$f(x) = x$，则下列结论中一定正确的是

A. $f(10) > 100$
B. $f(20) > 1000$
C. $f(10) < 1000$
D. $f(20) < 10000$

==========B==========

9、请完成下面一道选择题，在每小题给出的选项中，有一项或多项符合题目要求，请选出所有你认为正确的选项。
为了解推动出口后的亩收入（单位：万元）情况，从该种植区抽取样本，得到推动出口后亩收入的样本均值 $\overline{x} = 2.1$，样本方差 $S^2 = 0.01$，已知该种植区以往的亩收入 $x$ 服从正态分布 $N(1.8, 0.1^2)$，假设推动出口后的亩收入 $Y$ 服从正态分布 $N(\overline{x}, S^2)$，则（若随机变量 $Z$ 服从正态分布 $N(u, \alpha^2)$，则 $P(Z < u + \alpha) \approx 0.8413$）：

A. $P(x > 2) > 0.2$
B. $P(x > 2) < 0.5$
C. $P(Y > 2) > 0.5$
D. $P(Y > 2) < 0.8$

==========BC==========

10、请完成下面一道选择题，在每小题给出的选项中，有一项或多项符合题目要求，请选出所有你认为正确的选项。
设函数 $f(x) = (x-1)^2(x-4)$，则：

A. $x = 3$ 是 $f(x)$ 的极小值点
B. 当 $0 < x < 1$ 时 $f(x) < f(x^2)$
C. 当 $1 < x < 2$ 时，$-4 < f(2x-1) < 0$
D. 当 $-1 < x < 0$ 时，$f(2-x) > f(x)$

==========ACD==========

11、请完成下面一道选择题，在每小题给出的选项中，有一项或多项符合题目要求，请选出所有你认为正确的选项。
某造型可以看作图中的曲线 $C$ 的一部分。已知 $C$ 过坐标原点 $O$，且 $C$ 上的点满足横坐标大于 $-2$，到点 $F(2,0)$ 的距离与到定直线 $x = a$ ($a < 0$) 的距离之积为 $4$，则：
A. $a = -2$
B. 点 $(2\sqrt{2}, 0)$ 在 $C$ 上
C. $C$ 在第一象限的点的纵坐标的最大值为 $1$
D. 当点 $(x_0, y_0)$ 在 $C$ 上时，$y_0 \leq \frac{4}{(x_0 + 2)}$

==========ABD==========
```