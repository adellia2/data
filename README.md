import java.util.Scanner;

public class A2023_02_07_01 {
    public static void main(String[] args) {
        game();
    }
    public static void game(){
        Scanner sc = new Scanner(System.in);
        String player1,player2;//플레이어 이름
        int turn=0;//턴
        int num=0;//입력값
        int max=0; //정답
        int max8=0;//8의 배수
        int max8_1=0;
        int max10=0;//10의 배수
        int max10_1=0;
        boolean chance1=false;
        boolean chance1_1=false;
        int chance3=0;
        int turnChance=0;

        putNum(max);
        System.out.println("플레이어의 이름을 입력해 주십시오.");
        System.out.print("1번 플레이어 이름 입력: ");
        player1=sc.next().toString();
        System.out.print("2번 플레이어 이름 입력: ");
        player2=sc.next().toString();
        System.out.print(player1+","+player2+"님 반갑습니다.");

        rull();//경기 규칙 및 시작알림

        while (true){
            turn++;
            if(turnChance >0){turnChance--;}
            System.out.println("round:"+turn);

            max8(turn,max8,max,max8_1); // 8의 배수턴
            max10(turn,max10,max,max10_1);//10의 배수턴

            if(turn==1) { System.out.println(player1 + "님부터 시작합니다."); } //처음 시작만
            playerNum(player1,num,sc);
            upDown(num,max); //업 다운 출력

            if(num==max) { //정답을 맞힌 경우
                chance3=turn+5; // 5회 이내 체크용
                end(turn,player1); //찐 정답
                if(turn % 5==0){ max+=1200; //정답을 맞혔으나 5의 배수인 경우
                    chance1=true;}
                if(turn % 7==0){ max-=560;// 정답을 맞혔으나 7의 배수인 경우
                    chance1=true;}
            }
            else{
                if(chance1==true && turnChance <= 0){ //힌트 1
                    turnChance+=3;
                    int j=0;
                    hint1(max); //힌트1 j값 반환

                    hint3(j,max); //힌트3 max값 반환

                    if(j<=3){
                        turnChance+=1;
                    }
                    hint2(turn,chance3,turnChance); //힌트2 turnChance반환
                    hint4(max,turnChance);//힌트4 turnChance반환
                }
            }
            ////////////////////////////////////
            playerNum(player2,num,sc);
            upDown(num,max); //업 다운 출력

            if(num==max) { //정답을 맞힌 경우
                chance3=turn+5; // 5회 이내 체크용
                end(turn,player2); //찐 정답
                if(turn % 5==0){ max+=1200; //정답을 맞혔으나 5의 배수인 경우
                    chance1_1=true;}
                if(turn % 7==0){ max-=560;// 정답을 맞혔으나 7의 배수인 경우
                    chance1_1=true;}
            }
            else {
                if (chance1_1 == true && turnChance <= 0) { //힌트 1
                    turnChance += 3;
                    int j = 0;
                    hint1(max); //힌트1 j값 반환

                    hint3(j, max); //힌트3 max값 반환

                    if (j <= 3) {
                        turnChance += 1;
                    }
                    hint2(turn,chance3,turnChance); //힌트2 turnChance반환
                    hint4(max,turnChance);//힌트4 turnChance반환
                }
            }
        }
    }
    public static int putNum(int max){
        System.out.println("지금부터 게임을 진행합니다.");
        System.out.print("첫번째 숫자 입력: ");
        max(max);
        System.out.print("두번째 숫자 입력: ");
        max(max);
        System.out.print("세번째 숫자 입력: ");
        max(max);
        System.out.print("네번째 숫자 입력: ");
        max(max);
        System.out.println("번호 저장 완료.");

        System.out.println("자, 숫자는 제공되었고, 이제는 입력된 숫자가 모두 더해졌습니다.");
        System.out.println("우리는 그 답을 맞춰보도록 하겠습니다. 최대한 빠른 사람이 승리입니다.");

        return max;
    }
    public static void rull(){
        System.out.println("지금부터 게임을 진행할 것인데, 몇 가지 소소한 규칙을 정하도록 하겠습니다.\n" +
                "\n" +
                " \n" +
                "\n" +
                "규칙 1 : \n" +
                "\n" +
                "5의 배수 번째 턴에 정답을 입력한 경우 오답으로 표출 되며, 정답이 + 1200이 된다.\n" +
                "\n" +
                "7의 배수 번째 턴에 정답을 입력한 경우, 오답으로 표출 되며, 정답이 - 560이 된다.\n" +
                "\n" +
                " \n" +
                "\n" +
                "규칙 2 :\n" +
                "\n" +
                "만약 위 규칙 1번 때문에 아깝게 정답을 맞추지 못하는 사람의 턴[돌아오는 턴]에만, 아래 힌트가 제공된다.\n" +
                "\n" +
                " \n" +
                "\n" +
                "\t\n" +
                "\t힌트1. 힌트 1은 정답의 약수를 제공한다. 그러나 약수 중에서도 20이상의 숫자만 나타나야 하고,\n" +
                "\t약수의 개수가 최대 5개까지만 나올 수 있다. (약수가 5개 이하면 전부 나타난다.)\n" +
                "\n" +
                "\t\t예시)\t정답이 100인 경우\n" +
                "\n" +
                "\t\t\t정답이 20의 배수입니다.\n" +
                "\n" +
                "\t\t\t정답이 25의 배수입니다.\n" +
                "\n" +
                "\t\t\t정답이 50의 배수입니다.\n" +
                "\n" +
                "\t\t\t정답이 100의 배수입니다.\n" +
                "\n" +
                "\t\t\t더 이상 일치하는 배수가 없습니다.\n" +
                "\n" +
                "\t\t예시2) 정답이 50인 경우\n" +
                "\n" +
                "\t\t\t정답이 25의 배수입니다.\n" +
                "\n" +
                "\t\t\t정답이 50의 배수입니다.\n" +
                "\n" +
                "\t\t\t더 이상 일치하는 배수가 없습니다.\n" +
                "\n" +
                "\t힌트2. 최근 5턴 동안[서로 한 번씩 숫자를 입력하였을 경우가 한 턴]입력한 숫자 중에서,\n" +
                "\n" +
                "\t\t\t정답이 존재하는 경우, \"이전 최근 5턴 중에서 정답이 존재합니다\"\n" +
                "\n" +
                "\t\t\t정답이 존재하지 않는 경우, \"이전 최근 5턴 중에서 정답이 존재하지 않습니다.\"\n" +
                "\n" +
                "\t힌트3. 만약 위 힌트를 받고도, 정답을 못 풀었을 경우,\n" +
                "\n" +
                "\t\t\t다음 사람이 바로 정답을 맞추는 것을 방지하기 위해 아래 같은 조건이 나타난다.\n" +
                "\n" +
                "\t\t\t힌트1에서 나타난 값이 1개라면, 정답이 100이 +되고,\n" +
                "\n" +
                "\t\t\t힌트1에서 나타난 값이 3개라면, 정답이 360이 +되고,\n" +
                "\n" +
                "\t\t\t힌트1에서 나타난 값이 5개가 나타났다면, 정답이 1700이 +된다.\n" +
                "\n" +
                "\t\t\t단, \"더 이상 일치하는 배수가 없습니다\"라는 문구는 포함되지 않는다.\n" +
                "\n" +
                "\t힌트4. 힌트를 이미 받았는데, 정답을 못 맞추었다면, 패널티가 작동된다.\n" +
                "\n" +
                "\t\t패널티란, 이후로 ?턴동안, 힌트를 받을 수 없게 되는 패널티이다.\n" +
                "\n" +
                "\t\t힌트 1번에서 알려준 배수가 3개 미만이라면 해당 턴은 + 1이 된다.\n" +
                "\n" +
                "\t\t힌트 2번에서 5턴 중에 정답이 존재하였는데도 맞추지 못했다면 턴은 + 3이된다.\n" +
                "\n" +
                "\t\t힌트 3번에서 나온 값을 포함하여, 정답이 2000이상이라면, + 7턴이 된다.\n" +
                "\n" +
                "\t\t힌트 3번에서 나온 값이 2000 미만이라면 -9턴이 된다.\n" +
                "\n" +
                "\t\t기본 제공되는 패널티는 3턴이다.\n" +
                "\n" +
                "\n" +
                "규칙 3 : 8의 배수 번째 이후에도 정답이 나오지 않을 시 정답의 각 자리수 합을 힌트로 제공한다.\n" +
                "\n" +
                "\t예시) 정답이 2500일 경우 7을 제공.\n" +
                "\n" +
                " \n" +
                "\n" +
                "규칙 4 : 10턴의 배수 턴까지 정답이 나오지 않을 경우 정답의 자리수를 힌트로 제공한다.\n" +
                "\n" +
                "\t예시) 정답이 450일 경우 3자리 수로 힌트가 제공된다.");

        System.out.println("==============================================================================");
        System.out.println("1.플레이어가 제시한 숫자보다 크거나 작을 시 컴퓨터가 알려줍니다. 그럼 게임을 시작하겠습니다.");
    }
    public static int playerNum(String player1,int num,Scanner sc){
        System.out.print(player1+"님이 입력할 번호:");
        num=sc.nextInt();
        return num;
    }
    public static int max(int max){
        Scanner sc = new Scanner(System.in);
        int num=0;//입력값
        num=sc.nextInt();
        max+=num;

        return max;
    }
    public static int max8(int turn,int max8,int max,int max8_1){
        if(turn % 8==0){ //8의 배수턴
            max8=max;
            while(max8!=0){
                max8_1 += max8%10;
                max8 /=10;
            }
            System.out.println("각 자리수의 합은 "+max8_1+"입니다.");
        }
        return max8;
    }

    public static int max10(int turn,int max10,int max,int max10_1){
        if(turn % 10==0){ //10의 배수턴
            max10=max;
            max10_1=(int)(Math.log10(max10)+1);
            System.out.println("정답의 자리수는 "+max10_1+"입니다.");
        }
        return max10;
    }
    public static void upDown(int num,int max){
        if(num>max){System.out.println("정답은 입력하신 숫자보다 작습니다.");}
        if(num<max){System.out.println("정답은 입력하신 숫자보다 큽니다.");}
    }
    public static int hint1(int max){
        int j=0;
        for(int i = 20; i <= max; i++,j++){
            if(max % i == 0 &&j <= 5){
                System.out.println("정답이 "+i + "의 배수 입니다.");
            }
        }
        if(j!=1 || j!=3 ||j!=5) {
            System.out.println("더 이상 일치하는 배수가 없습니다.");
        }
        return j;
    }
    public static int hint2(int turn,int chance3,int turnChance){
        if (chance3 >= (turn)) { //힌트 2
            System.out.println("이전 최근 5턴 중에서 정답이 존재합니다.");
            turnChance += 3;
        } else {
            System.out.println("이전 최근 5턴중에서 정답이 존재하지 않습니다.");
        }
        return turnChance;
    }

    public static int hint3(int j,int max){
        if(j==1){max+=100;System.out.println("정답이 +100되었습니다.");} //힌트 3
        if(j==3){max+=360;System.out.println("정답이 +360되었습니다.");}
        if(j==5){max+=1700;System.out.println("정답이 +1700되었습니다.");}

        return max;
    }
    public static int hint4(int max,int turnChance){
        if (max <= 2000) { //힌트 4
            turnChance -= 9;
        }
        return turnChance;
    }
    public static void end(int turn,String player1){
        if (turn%5 != 0 && turn%7 != 0) { //찐 정답
            System.out.println("정답입니다!! 완벽하십니다!! 멋지세요!!");
            System.out.println(player1 + "님 승리!!");
            System.exit(1);
        }
    }

}
