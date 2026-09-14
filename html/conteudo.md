Estava estudando aqui e pensando, pelo que entendi o Node possui apenas uma Thread e ele processas as coisas "sincronas" e nao "Assincronas" como ocorre em Java, e outras linguagems. Ele delega as coisas para o C++/SO para que eles processam arquivos pesados e possa liberar as sua thread para outros usuarios usarem, por isso ele consegue processar mihares de requisicoes sem quebrar ou cair. Aguentando. O que eles fazem muito é usar o always/await para ele esperar uma request antes de fazer a proxima operacao, porem ele libera a thread para os outros processos que estao na stack Trace (pilha de execucao). Contudo o objetivo dele entao é ter micro processos que rodam tao rapidos, consumindo a pilha de execucao com o event loop e chamando novamente (passando o resultado para a thread original) a thread original que da a impressao de ser assincrono, porem ele é sincrono. Nas outras linguagens cada usuario cria uma thread para ele, por isso ele acaba caindo quando ocorre um numero de requisicoes elevadas. Node tem uma compilacao em JIT (just in Time)

v8 Engine (compilacao JIT C++)
    l-> Mesmo motor do chrome, escrito em C
Libuv (Event Loop/I/O)
APIs de sistema(fs,http, crypto, path, etc.)



Estava estudando e percebi algo legal, a diferença clara entre o SSR (Server Side Rendering) e o SSG(server site Generation) 
o que muda -> SSR ele é um conteudo que é estatico, ou seja, ele é criado o html estatico e quando precisar alterar alguma coisa, acessar o servidor ou algo do tipo, ele faz uma pequena requisicao para o servidor so para recuperar alguma informacao mas sem atualizar a pagina inteira. Ja o SSG ele é dinamico, ou seja, ele se trabalha com rotas, o que a gente fez no exercicio html/index.html e no html/construtor.js ele espera uma chamada de uma rota com um metodo especifico, ao ser chamado o node intercepta o dado e chama o metodo existente para aquela rota e para aquele metodo para fazer o carregamento do html dinamicamente para o usuario. Normalmente é carregado um Js invisivel junto para ele fazer as request pro servidor via API usando JSON pedindo a pagina que quer mostrar e recebendo a resposta.   

