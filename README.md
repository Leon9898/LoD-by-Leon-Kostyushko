# LoD-by-Leon-Kostyushko
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.ArrayList;


public class HttpURLConnectionExample {

    private final String USER_AGENT = "Mozilla/5.0";

    public static void main(String[] args) throws Exception {

        HttpURLConnectionExample http = new HttpURLConnectionExample();

        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        int minutes = Integer.parseInt(reader.readLine());    // minutes - отвечает за кол-во последних минут, о событиях которых программа выведет результат

        int maleCount = 0;
        int femaleCount = 0;

        for(int j = 0; j < minutes; j++) {
            String newLine = http.sendGet().substring(1, http.sendGet().length() - 1);

            newLine += ";;";


            System.out.println(newLine);

            ArrayList<Character> list = new ArrayList<Character>();
            for (int i = 0; i < newLine.length(); i++) list.add(newLine.charAt(i));

            while (list.get(0) != ';') {
                if (list.get(0) == 'M') {
                    if (list.get(5) == 'B') maleCount++;
                    else maleCount--;

                    for (int i = 0; i <= 9; i++) list.remove(0);

                } else {
                    if (list.get(7) == 'B') femaleCount++;
                    else femaleCount--;

                    for (int i = 0; i <= 11; i++) list.remove(0);
                }

            }

            Thread.sleep(60000);

        }
        System.out.println(maleCount);
        System.out.println(femaleCount);




















    }


    private String sendGet() throws Exception {



        String url = "http://api.lod-misis.ru/testassignment";

        URL obj = new URL(url);
        HttpURLConnection con = (HttpURLConnection) obj.openConnection();


        BufferedReader in = new BufferedReader(
                new InputStreamReader(con.getInputStream()));
        String inputLine;
        StringBuffer response = new StringBuffer();

        while ((inputLine = in.readLine()) != null) {
            response.append(inputLine);
        }
        in.close();


        return response.toString();




    }
}
