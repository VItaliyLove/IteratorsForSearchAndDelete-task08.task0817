#Solution for JavaRush task #0817;

package com.javarush.task.task08.task0817;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;
/* 
Нам повторы не нужны
*/


public class Solution {

    public static HashMap<String, String> createMap() {
        HashMap <String,String> list = new HashMap<String,String>();
        list.put("Stark",     "Sansa");
        list.put("Stak",      "Sansa");
        list.put("Barateon",  "Stanis");
        list.put("Snow",      "John");
        list.put("Lannister", "Jeime");
        list.put("Dow",       "John");
        list.put("Targarien", "Reigar");
        list.put("Martell",   "Sasa");
        list.put("Sivort",    "Davos");
        list.put("Greygoi",   "Teon");
        list.put("Mormont",   "Jorah");
        return list;
    }

    public static void removeTheFirstNameDuplicates(Map<String, String> map) {
        Iterator<HashMap.Entry<String,String>> first = map.entrySet().iterator();
        /*определяем позиции для итераторов по которым будем выставлять их на место поле операции удаления*/
        int positionForFirstIter = 0; 
        int positionForSecondIter = 0;
        while(first.hasNext()) // начинаем цикл первого итератора
        {
            Iterator<HashMap.Entry<String,String>> second = map.entrySet().iterator(); // инициализируем второй итератор
            positionForSecondIter = positionForFirstIter+1; // его позиция должна быть на одну больше чем у первого итератора
            /*цикл по которому выставляем итератор на его место*/
            for (int i = 0; i < positionForSecondIter; i++) {
                second.next();
            }

            boolean del = false; // индикация налчия операции удаления
            String temp = first.next().getValue(); // забираем .value первого итератора во временную переменную
            
            /*начинаем цикл второго итератора*/
            while(second.hasNext()) {
                if (second.next().getValue().equals(temp)) { // если совпадение
                    second.remove(); // удаляем
                    del = true; // индикация наличия операции удаления
                }
            }

            if (del) {
                first = map.entrySet().iterator(); // заново инициализируем первый итератор
                /*/*цикл по которому выставляем итератор на его место*/
                for (int i = 0; i < positionForFirstIter; i++) {
                    first.next();
                }
                /*шаг вперёд на удаляемое значение*/
                first.next();
                first.remove();
            }
            else {
                positionForFirstIter++;
            }
        }
        removeItemFromMapByValue(map, "a");
    }

    public static void removeItemFromMapByValue(Map<String, String> map, String value) {
        HashMap<String, String> copy = new HashMap<String, String>(map);
        for (Map.Entry<String, String> pair : copy.entrySet()) {
            if (pair.getValue().equals(value))
                map.remove(pair.getKey());
        }

    }

    public static void main(String[] args) {
        HashMap<String,String> myMap = createMap();
        removeTheFirstNameDuplicates(myMap);
        for (Map.Entry<String, String> s : myMap.entrySet()) {
            System.out.println(s.getKey() + " " + s.getValue());
        }
    }
}
