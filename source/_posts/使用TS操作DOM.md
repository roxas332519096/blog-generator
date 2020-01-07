---
title: 使用TS写一个计算器
date: 2020-01-07 17:28:19
categories:
- TS
tags:
- TS
---

1. 将TS热更新为JS

```
tsc -w demo.ts
```

在html里引入demo.js

2. 主要代码

``` bash
{

    class Calculator {
        public container: HTMLDivElement
        private output: HTMLDivElement
        private span: HTMLSpanElement
        public n1: string = null
        public n2: string = null
        public result: string = null
        public operator: string;
        public keys: Array<Array<string>> = [
            ['clear', '÷'],
            ['7', '8', '9', 'X'],
            ['4', '5', '6', '-'],
            ['1', '2', '3', '+'],
            ['0', '.', '=']
        ]
        constructor() {
            this.createContainer()
            this.createOutput()
            this.createButtons()
            this.bindEvents()
        }
        createButton(text: string, container: HTMLElement, className: string) {
            const button: HTMLButtonElement = document.createElement('button')
            button.textContent = text
            button.classList.add('button')
            if (className) {
                button.classList.add(className)
            }
            container.appendChild(button)
            return button
        }
        createButtons() {
            this.keys.forEach((textList: Array<string>) => {
                const div: HTMLDivElement = document.createElement('div')
                div.classList.add('row')
                textList.forEach((text: string) => {
                    this.createButton(text, div, `text-${text}`)
                })
                this.container.appendChild(div)
            })
        }
        createContainer() {
            const container: HTMLDivElement = document.createElement('div')
            container.classList.add('calculator')
            document.body.appendChild(container)
            this.container = container
        }
        createOutput() {
            const output: HTMLDivElement = document.createElement('div')
            output.classList.add('output')
            const span: HTMLSpanElement = document.createElement('span')
            span.textContent = '0'
            output.appendChild(span)
            this.container.appendChild(output)
            this.output = output
            this.span = span
        }
        bindEvents() {
            this.container.addEventListener('click', (e) => {
                if (e.target instanceof HTMLButtonElement) {
                    const button: HTMLButtonElement = e.target
                    const text: string = button.textContent
                    this.update(text)
                }
            })
        }
        update(text: string) {
            if ('0123456789.'.indexOf(text) >= 0) {
                this.updateNumbers(text)
            } else if ('+-X÷'.indexOf(text) >= 0) {
                if (this.n1 === null) {
                    this.n1 = this.result
                }
                this.operator = text
            } else if (text === '=') {
                this.updateResult()
            } else if (text === 'clear') {
                this.n1 = null
                this.n2 = null
                this.result = null
                this.operator = null
                this.span.textContent = '0'
            }
        }
        updateNumbers(text: string) {
            if (this.operator) {
                this.updateNumber('n2', text)
            } else {
                this.updateNumber('n1', text)
            }
        }
        updateNumber(name: string, text: string) {
            if (this[name]) {
                this[name] += text
            } else {
                this[name] = text
            }
            this.span.textContent = this[name].toString()
        }
        updateResult() {
            let result: any;
            let n1: number = parseFloat(this.n1)
            let n2: number = parseFloat(this.n2)
            switch (this.operator) {
                case '+':
                    result = n1 + n2
                    break
                case '-':
                    result = n1 - n2
                    break
                case 'X':
                    result = n1 * n2
                    break
                case '÷':
                    result = n1 / n2
                    break
            }
            if (n2 === 0) {
                result = '不是数字'
            }
            this.span.textContent = result
            this.n1 = null
            this.n2 = null
            this.result = result
        }
    }

    new Calculator()
}

```