# pukea
bidaxiao
public class Card {
    public String number;
    public String color;

    public Card(String color,String number) {
        super();
        this.number = number;
        this.color = color;
    }

    public String getNumber() {
        return number;
    }

    public String getColor() {
        return color;
    }   
}



public class Compara implements Comparator<Card>{

    @Override
    public int compare(Card arg0, Card arg1) {
        String color="黑桃  红桃 梅花 方块";
        String numbers="2 3 4 5 6 7 8 9 10 J Q K A";

        int result=numbers.indexOf(arg0.number)-numbers.indexOf(arg1.number);

        if(result<0){
            return -1;
        }else if(result>0){
            return 1;
        }else {
            int result2=color.indexOf(arg0.color)-color.indexOf(arg0.color);
            if(result2>0){
                return 1;
            }else if(result<0){
                return -1;
            }else{
                return 0;
            }
        } 
    }
}

public class GameBegin {

    private static Scanner console=new Scanner(System.in);
    private Random random=new Random();
    private List<Card> cardsList=new ArrayList<Card>();
    private static Player playA;
    private static Player playB;

    public static void main(String[] args) {
        GameBegin gb=new GameBegin();
        gb.createCardsList();

        System.out.println("hello,player A ,please input you name:");
        String nameA=console.next();
        playA=gb.getPlayer(nameA);

        System.out.println("\nhello,player B ,please input you name:");
        String nameB=console.next();
        playB=gb.getPlayer(nameB);

        gb.lastTEST();
    }


    public List<Card> createCardsList(){
        String[] color={"黑桃","红桃","梅花","方块"};
        String[] numbers={"2","3","4","5","6","7","8","9","10","J","Q","K","A"};
        for(String temp:color){
            for(int i=0;i<numbers.length;i++){
                Card card=new Card(temp,numbers[i]);
                cardsList.add(card);
            }
        }
        mixCardsList();
        return cardsList;
    }

    private void mixCardsList(){
         Collections.shuffle(cardsList);
    }

    public Player getPlayer(String name){
        Player play=new Player(name);
        for(int i=0;i<2;i++){
            play.list.add(cardsList.get(getRandomNumber()));
        }
        outputPlayerCards(play);
        return play;
    }


    private int getRandomNumber(){
        int k;
        k=random.nextInt(51);
        return k;
    }

    private void outputPlayerCards(Player play){
        System.out.print("Player you got:");
        for(Card c:play.list){
            System.out.print(c.getColor()+" "+c.getNumber()+"   ");
        }
        Collections.sort(play.list,new Compara());
        System.out.println("  the biger card is :"+play.list.get(1).color+" "+play.list.get(1).number);
    }

    public void lastTEST(){
        List<Card> lastCards=new ArrayList<Card>();
        lastCards.add(playA.list.get(1));
        lastCards.add(playB.list.get(1));
        Collections.sort(lastCards,new Compara());
        System.out.println("the biger card is: "+lastCards.get(1).color+lastCards.get(1).number);

        if(lastCards.get(1).color.equals(playA.list.get(1).color)){
            System.out.println("\n"+playA.name+" is win!");
        }else{
            System.out.println("\n"+playB.name+" is win!");
        }
    }
    }
