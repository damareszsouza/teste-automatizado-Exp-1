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
