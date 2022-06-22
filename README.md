# teste-automatizado-Exp-1
Exemplo de codigo de um leilão - replica do livro teste automatizado de software um guia pratico

Teste maior de todos exemplo de código Java

class Avaliador {

private double maiorDeTodos = Double.NEGATIVE_INFINITY;
public void avalia(Leilao leilao) {
for(Lance lance : leilao.getLances()) {
if(lance.getValor() > maiorDeTodos) {
maiorDeTodos = lance.getValor();
}
}
}
public double getMaiorLance() {
return maiorDeTodos;
}
}
class TesteDoAvaliador {
public static void main(String[] args) {
Usuario joao = new Usuario("Joao");
Usuario jose = new Usuario("José");
Usuario maria = new Usuario("Maria");
Leilao leilao = new Leilao("Playstation 3 Novo");
leilao.propoe(new Lance(joao,300.0));
leilao.propoe(new Lance(jose,400.0));
leilao.propoe(new Lance(maria,250.0));
Avaliador leiloeiro = new Avaliador();
leiloeiro.avalia(leilao);
// imprime 400.0
System.out.println(leiloeiro.getMaiorLance());
}
}

Implementando uma nova funcionalidade
A próxima funcionalidade a ser implementada é a busca pelo menor lance de
todos. Essa regra de negócio faz sentido estar também na classe Avaliador.
Basta acrescentarmos mais uma condição, desta vez para calcular o menor
valor:
class Avaliador {
private double maiorDeTodos = Double.NEGATIVE_INFINITY;
private double menorDeTodos = Double.POSITIVE_INFINITY;
public void avalia(Leilao leilao) {
for(Lance lance : leilao.getLances()) {
if(lance.getValor() > maiorDeTodos) {
maiorDeTodos = lance.getValor();
}
else if(lance.getValor() < menorDeTodos) {
menorDeTodos = lance.getValor();
}
}
}
public double getMaiorLance() { return maiorDeTodos; }
public double getMenorLance() { return menorDeTodos; }
}
class TesteDoAvaliador {
public static void main(String[] args) {
Usuario joao = new Usuario("Joao");
Usuario jose = new Usuario("José");
Usuario maria = new Usuario("Maria");

Leilao leilao = new Leilao("Playstation 3 Novo");
leilao.propoe(new Lance(joao,300.0));
leilao.propoe(new Lance(jose,400.0));
leilao.propoe(new Lance(maria,250.0));
Avaliador leiloeiro = new Avaliador();
leiloeiro.avalia(leilao);
// imprime 400.0
System.out.println(leiloeiro.getMaiorLance());
// imprime 250.0
System.out.println(leiloeiro.getMenorLance());
}
}

Tudo parece estar funcionando. Apareceram na tela o menor e maior
valor corretos. Vamos colocar o sistema em produção, afinal está testado!
Mas será que o código está realmente correto? Veja agora um outro teste,
muito parecido com o anterior:
class TesteDoAvaliador {
public static void main(String[] args) {
Usuario joao = new Usuario("Joao");
Usuario jose = new Usuario("José");
Usuario maria = new Usuario("Maria");
Leilao leilao = new Leilao("Playstation 3 Novo");
leilao.propoe(new Lance(maria,250.0));
leilao.propoe(new Lance(joao,300.0));
leilao.propoe(new Lance(jose,400.0));
Avaliador leiloeiro = new Avaliador();
leiloeiro.avalia(leilao);
// imprime 400.0

System.out.println(leiloeiro.getMaiorLance());
// INFINITY
System.out.println(leiloeiro.getMenorLance());
}
}

Um teste automatizado é muito parecido. Você sempre executa estes três
passos: monta o cenário, executa a ação e valida a saída. Mas, acredite ou
não, já escrevemos algo muito parecido com um teste automatizado neste
capítulo. Lembra da nossa classe TesteDoAvaliador? Perceba que ela se
parece com um teste, afinal ela monta um cenário e executa uma ação. Veja o
código:


class Teste {
public static void main(String[] args) {
// cenario: 3 lances em ordem crescente
Usuario joao = new Usuario("Joao");
Usuario jose = new Usuario("José");
Usuario maria = new Usuario("Maria");
Leilao leilao = new Leilao("Playstation 3 Novo");
leilao.propoe(new Lance(maria,250.0));
leilao.propoe(new Lance(joao,300.0));
leilao.propoe(new Lance(jose,400.0));
// executando a ação
Avaliador leiloeiro = new Avaliador();
leiloeiro.avalia(leilao);
// exibindo a saída
System.out.println(leiloeiro.getMaiorLance());
System.out.println(leiloeiro.getMenorLance());
}
}

Para melhorar isso, precisamos fazer a própria máquina verificar o resul-
tado. Para isso, ela precisa saber qual a saída esperada. Ou seja, a máquina
deve saber que o maior esperado, para esse caso, é 400, e que o menor es-
perado é 250. Vamos colocá-la em uma variável e então pedir pro programa
verificar se a saída é correta:
class TesteDoAvaliador {
public static void main(String[] args) {
// cenário: 3 lances em ordem crescente
Usuario joao = new Usuario("Joao");
Usuario jose = new Usuario("José");
Usuario maria = new Usuario("Maria");
Leilao leilao = new Leilao("Playstation 3 Novo");
leilao.propoe(new Lance(maria,250.0));
leilao.propoe(new Lance(joao,300.0));
leilao.propoe(new Lance(jose,400.0));
// executando a ação
Avaliador leiloeiro = new Avaliador();
leiloeiro.avalia(leilao);
// comparando a saída com o esperado
double maiorEsperado = 400;
double menorEsperado = 250;
System.out.println(maiorEsperado ==
leiloeiro.getMaiorLance());
System.out.println(menorEsperado ==
leiloeiro.getMenorLance());
}
}
Ao rodar esse programa, a saída já é um pouco melhor:
true
false
