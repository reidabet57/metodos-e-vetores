
import java.util.Scanner;

class Main {

  static Scanner console = new Scanner(System.in);
  

  static final int TOTAL_AVALIACOES = 4;
  static final String[] NOMES_AVALIACOES = { "A1", "A2", "A3", "AI" };
  static final double[] NOTA_MAX_AVALIACOES = { 30.00, 30.00, 40.00, 30.00};
  
  static double[] notas = new double [TOTAL_AVALIACOES];

     
  
  
  /**
	 * Ler uma nota do usuário
	 * @param mensagem O texto que aparecerá na tela
	 * @return um número double representando a nota.
	 */
	static double lerNota(String mensagem, double notaMaxima) {

      double nota = 0.0;

      do {

        System.out.printf("%s = ", mensagem);
        nota = console.nextDouble();
        
      } while (nota < 0.00 || nota > notaMaxima);

    return nota;
	}

  
  /**
  * Atualiza o valor da respectiva nota do estudante
  * @param indiceNota um número inteiro representando o índice (posição) da nota no vetor
  */
  static void atualizarNota(int indiceNota) {

    System.out.println();
    notas[indiceNota] = lerNota(NOMES_AVALIACOES[indiceNota], NOTA_MAX_AVALIACOES[indiceNota]);
  
  } // Fim do método atualizarNota

  
 /**
  * @param notaFinal A soma de todas as avalições feita pelo estudante ao longo do semestre
  * @return uma string representando o status final do estudante, são eles: APROVADO, REPROVADO, EM RECUPERAÇÃO.
  */
  static String avaliarSituacao(double notaFinal) {

    if(notaFinal < 30)
      return "REPROVADO";
    else if (notaFinal < 70)
      return "EM RECUPERAÇÃO";
    else
      return "APROVADO";
    
  } // Fim do método avaliarSituacao()
  

  static double calcularMedia(double[] notas) {
		
	  double media = 0.0d;
	  
	double A1 = notas[0];
	double A2 = notas[1];
	double A3 = notas[2];
	return (A1+A2+A3)/3;
	
  } // Fim do método calcularMedia()
	
  static String maiorNota(double[] notas) {
	   	  
	  if ((notas[0] > notas[1])&&( notas[0] > notas[2])) 
	  return "\n  Maior nota do semestre = " + notas[0];
	 
	  if((notas[1] > notas[0])&&(notas[1] > notas[2])) 
	  return "\n  Maior nota do semestre = " + notas[1];
	  
      if((notas[2] > notas[0])&&(notas[2] > notas[1])) 
      return "\n  Maior nota do semestre = " + notas[2];
      
   	  return "";
   
  } // Fim do método maiorNota()
    
 
  static double fazerIntegrada(double[] notas) {
	  
	  Scanner AI = new Scanner (System.in);
	  
	  
	  double avaliacao = notas[3];
	  double notaFinal = notas[0]+notas[1]+notas[2];
	
	  if (notaFinal < 70 && notaFinal >= 30) {
	  System.out.println("\n  O aluno necessita realizar a Avaliação Integrada, pois ficou EM RECUPERAÇÃO.");
	  System.out.printf("\n  Digite a nota da Avaliação Integrada: "); 
	  } else System.out.println("\n  Parabéns!");
	  
	  avaliacao = AI.nextDouble();
	  if (avaliacao > 30) {
		  System.err.println("\n Valor inválido"); }
	  
	  double menorNotaA1 = avaliacao+notas[2]+notas[1];
      double menorNotaA2 = avaliacao+notas[0]+notas[2];
    
		  if((notas[0] < notas[1]) &&(notas[0] < notas[2])) {
		  System.out.println("\n  Avaliação Integrada vai substituir a nota A1 que foi a menor nota.");
		  return       menorNotaA1; }

		   if ((menorNotaA1 >= 70)) {
		  System.out.println("\n Aluno Aprovado.");  }
		   else { System.out.println("\n Aluno Reprovado.");
		   } 
		   
		 
		  if ((notas[1] < notas[0])&&(notas[1] < notas[2])) {
		  System.out.println("\n  Avaliação Integrada vai substituir a nota A2 que foi a menor nota.");
		  return       menorNotaA2; }
		  
		  { if ((menorNotaA2 >= 70)) { 
			  System.out.println("\n Aluno Aprovado."); }
			   else  System.out.println("\n Aluno Reprovado.");
		  }
		
		  return 0;
	
	  } // Fim do método fazerAI()
       
 

  /**
  * Mostra na tela um relatório das notas do estudante
  */
  static void mostrarNotas() {

    double notaFinal = 0.0;

    System.out.println("\n\t\tNOTAS");
    System.out.println();

    for (int i = 0; i < TOTAL_AVALIACOES; i++) {

      System.out.printf("Avaliação %s = %.2f pts", NOMES_AVALIACOES[i], notas[i]);
      System.out.println();
      notaFinal += notas[i];
    
    }
    

    System.out.printf("\n  Nota Final = %.2f pts", notaFinal);
    System.out.printf("\n  Situação = %s ", avaliarSituacao(notaFinal));

    System.out.println("\n  Média Semestral = " + calcularMedia(notas));
    
    
    System.out.println(maiorNota(notas)); 
  
   
    System.out.println(fazerIntegrada(notas));
    
    
  
    

  } // Fim do método mostrarNotas()

  



/**
  * Exibe o menu principal da aplicação
  */
  static void mostrarMenu() {

    System.out.println("\n\n");
    System.out.println("\t\tMENU");
    System.out.println();
    
    System.out.println("[1] Cadastrar Notas A1");
    System.out.println("[2] Cadastrar Nota A2");
    System.out.println("[3] Cadastrar Nota A3");
    System.out.println("[4] Mostrar Notas");
    System.out.println("[0] SAIR");

    System.out.print("\nDigite uma opção:  ");
    byte opcao = console.nextByte();


    switch(opcao) {

      case 0:
        System.exit(0);
        break;
      
      case 1:
        atualizarNota(0);
        break;
      
      case 2:
        atualizarNota(1);
        break;

      case 3:
        atualizarNota(2);
        break;

      case 4:
        mostrarNotas();
        break;   
      
      default:
        mostrarMenu();
        break;

    }

    mostrarMenu();

  } // Fim do método mostrarMenu()

  
  public static void main(String[] args) {
    
    mostrarMenu();
  
  } // Fim do método main();
  
} // Fim da classe Main

