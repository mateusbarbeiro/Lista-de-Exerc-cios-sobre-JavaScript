# Lista de Exercios-sobre-JavaScript

1. O que é o ES6?
    - ES6, ECMAScript 6 ou ES2015, é o nome atribuido a padronização/especificação utilizada para implementar a linguagem JavaScript.

2. Exemplifique algumas features introduzidas no ES6.
   - Declaração de variáveis:
   
      adição de uma nova forma de declarar variaveis atraves dos termos var, let e const; 
      ```
       var a = 1;
       let b = 2;
       const c = 3;
       ```
    - Parâmetro de funções

      introduzido possibilidade de passar parametros com valores padrões atribuidos.
      ```
      const multiply = (x, y = 1) => x * y

      multiply(3) // 3
      ```
        introduzido os Rest Parameters "...", possibilita pegar todos os parâmetros de uma função como o objeto "arguments", porém corrigindo alguns dos problemas deste. 
      ```
      function sum(...numbers) {
        let result = 0
        numbers.forEach((number) => {
          result += number
        })
        return result
      }
      sum(1, 2, 3, 4, 5) // 15
      ```
    - Programação Funcional:

      introduzido arrows functions, uma maneira mais curta de declarar uma função.

      Convencional
      ```
      var sum = function(x, y) {
        return x + y;
      };

      sum(1, 2); // 3
      ```
      Com arrow function
      ```
      const sum = (x, y) => x + y
      sum(1, 2) // 3
      ```

      introduzido a descontrução (destructuring) de objetos e arrays, possibilitando a atribuição dos valores a variaveis. Uma nova forma de delarar variaveis.

      Com arrays
      ```
      const [a, b] = [5, 2]
      console.log(a) // 5
      console.log(b) // 2
      ```

      Com objetos
      ```
      const person = { name: 'Mateus', age: 19 }

      const {name, age} = person

      console.log(name) // 'Mateus'
      console.log(age) // 19
      ```
    - Orientação a Objetos

      introduzido classes, construtor, getters/setters e herança. 
      ```
      class Animal {
        constructor(name) {
          this._name = name
        }

        get name() {
          return this._name
        }

        set name(name) {
          this._name = name
        }

        speak() {
          console.log(`${this._name} makes a noise`)
        }
      }

      class Dog extends Animal {
        speak() {
          console.log(`${this._name} barks`)
        }
      }

      const dog = new Dog('Rex')
      dog.speak() // Rex barks
      ```
    - Módulos

      introduzido possibilidade de importar (import) e exportar (export) componentes possibilitando aumentar o reuso de código. 
      ```
      // lib.js
      export function sum(x, y) {
        return x + y
      }
      ```
      ```
      // test.js
      import { sum } from 'lib'
      sum(1, 2) // 3
      ```
      quando se exporta apenas uma função/classe por aquivo, se faz uso do termo "default". Sendo assim ao importar o módulo, o desenvolvedor pode atribuir o nome que bem quiser para ele.
      ```
      // square.js
      export default function (x) {
        return x * x
      }
      ```
      ```
      // test.js
      import square from 'square'
      square(2) // 4
      ```
    
3. Qual a diferença entre var, let e const?
    - var tem escopo de função. é içada(hosting) e automaticamente inicializada com o valor undefined, caso nao receba nenhum valor.
    - let tem escopo de bloco. assim como var, seu valor é undefined ao ser inicializado e nao atribuido nenhum valor.
    - const tem escopo de bloco. é utilizado para declarar constantes, ou seja, uma vez atribuido um valor para este, não se pode alterar mais. deve ser inicializada obrigatoriamente no momento de sua declaração.

4. O que é destructuring e para quais propósitos pode ser utilizado?
    - é uma nova forma de se declarar variaveis, extraindo seus valores direto de objetos ou arrays. é utilizado para reduzir repetições de codigo, deixando mais facil chamar atributos de objetos por exemplo.
      pode ser utilizado tanto para declarar variáveis quanto para atribuir valores a variaveis;

5. O que é o DOM?
     - modelo de Objeto de Documento  (DOM) é uma interface de programação para documentos HTML, XML e SVG. fornece uma representação estruturada do documento como uma árvore.
     Define metodos que permitem acesso, e manipul a arvore, como a alteração de estrutura e estilo do documento. ele conecta páginas web a scripts ou linguagens de programação.

6. Quais problemas o JavaScript assíncrono soluciona?
    - quando se precisa aguardar o processamento de alguns dados ou que algum evento ocorra antes de utilizar estes dados, é preciso se utilizar de programação assincrona, ou seja, é 
    preciso aguardar a execução de algum processo para então continuar a execução de uma tarefa seguinte.

7. Para que servem os comandos async e await?
    - são termos que simplificam a programação assíncrona, possibilitando a escrita de código de uma maneira sincrona, porem que funciona de forma assincrona. ao definir uma função como 
    async é preciso utilizar do termo await antes da chamada de uma expressão que retorne uma promessa, fazendo com que a execução seja pausada ate que a promessa seja resolvida.

8. Quais as vantagens de se usar Promises ao invés de callbacks?
    - o modelo de promises possibilita a gerência de retorno de valores e excessões. A vantagem de implementar promises é que seu retorno será uma variável.

9. Uma requisição a um servidor é feita, caso o valor enviado para o servidor seja uma cadeia de caracteres, o mesmo devolve essa cadeia de caracteres em caixa-alta, caso contrário um erro é devolvido informando “the request value is not supported”. Implemente uma Promise que simule o caso descrito e implemente um teste para o caso de sucesso e de erro. Além disso, a simulação deve conter um atraso aleatório de 500 milissegundo a 2 segundos, simulando o atraso da comunicação com o servidor. Dica: pesquisar sobre a função setTimeout.
      ```
      function getRandom(min, max) {
          return Math.random() * (max - min) + min;
      }

      function request(st) {
          return new Promise((resolve, reject) => {
              let queryResult

              console.log('waiting for request')
              setTimeout(() => {
                      if (typeof st === "string") {
                          queryResult = {
                              status: 200,
                              data: st.toUpperCase()
                          }
                      } else {
                          queryResult = {
                              status: 404,
                              data: 'the request value is not supported'
                          }
                      }
                      if (queryResult.status === 200) resolve(queryResult)
                      else reject(queryResult)
                  },
                  getRandom(500, 2000)
              )
          })
      }

      request(1234)
          .then(e => {
              const { data } = e
              console.log(`\nMaiúsculo: ${data}`)
          })
          .catch(e => {
              const { status, data } = e
              if (status === 404) console.log(`\n${status}: ${data}`)
          })

      request("mateus lindão")
          .then(e => {
              const { data } = e
              console.log(`\nMaiúsculo: ${data}`)
          })
          .catch(e => {
              const { status, data } = e
              if (status === 404) console.log(`\n${status}: ${data}`)
          })
      ```

10. Uma empresa de luz precisa de um software que monitore o estado das lâmpadas (acesa, apagada) instaladas nos postes de energia. Considerando que esses postes possuem lâmpadas inteligentes que acendem durante a noite e mantêm-se apagadas durante o dia. Saber se estão de fato acesas ou apagadas seriam de grande valor pois assim seria possível identificar lâmpadas queimadas. Desta forma, implemente uma função que, a cada intervalo aleatório de tempo entre 2 e 4 segundos, troque o estado da lâmpada e retorne para um callback que deve exibir no console o estado atual da lâmpada. Dica: pesquisar sobre a função setInterval.
      ```
      function numRandom(min, max) {
          return Math.random() * (max - min) + min;
      }

      function monitoringLight() {
          var stateLight = false

          setInterval(() => {
              stateLight = stateLight ? false : true
              console.log(stateLight ? "Aceso" : "Apagada")
          },
              numRandom(2000, 4000)
          )
      }

      monitoringLight()
      ```
11. Um professor de algoritmos está ensinando seus alunos a implementarem árvores binárias e cobra o seguinte exercício: “Implemente uma árvore binária cujo nó raiz seja um número qualquer. A árvore deve conter um método para criar 2 nós folha à direita e à esquerda do nó raiz, sendo ambos números quaisquer diferentes do valor do nó raiz e a estrutura deve automaticamente colocar o maior número informado à direita do nó raiz e o menor número informado à esquerda.” Implemente o exercício descrito acima usando as classes JavaScript. Deverá haver uma classe “Folha”, uma classe “No” e uma classe “Arvore”. A classe “Arvore” deve ser responsável por criar o nó raiz e deve conter o método que cria os nós folha baseados nos critérios do exercício descrito. Além disso, deve haver um modo de checar se o nó é um nó folha ou não e na execução da aplicação teste devem haver console.log’s informando o nó raiz e seus filhos e quais os tipos de cada nó (nó ou nó folha). Use conceitos de OO tais como herança.
