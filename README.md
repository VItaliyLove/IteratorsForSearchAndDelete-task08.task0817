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
        HashMap <String,String> list = new HashMap<String,String>()
        list.put("a","aa"); //1
        list.put("b","bb"); //2
        list.put("c","cc"); //3
        list.put("d","dd"); //4
        list.put("e","ee"); //5
        list.put("f","ii"); //6
        list.put("g","gg"); //7
        list.put("h","hh"); //8
        list.put("i","ii"); //9
        list.put("j","aa"); //10
        return list;
    }

    public static void removeTheFirstNameDuplicates(Map<String, String> map) {
        Iterator<HashMap.Entry<String,String>> first = map.entrySet().iterator(); // инициализируем первый итератор
        while(first.hasNext()) // цикл первого итератора
        {
            boolean del = false; // индикация наличия операции удаления
            String temp = first.next().getValue(); // сохраняем значение первого итератора в переменную
            Iterator<HashMap.Entry<String,String>> second = first; // инициализируем второй итератор
            while(second.hasNext()) // цикл второго итератора
            {
                if(second.next().getValue().equals(temp)) // если совпадение
                {
                    second.remove();
                    del = true; // наличие операции удаления
                }
            }
            if(del) // если была операция удаления
            {
                first = map.entrySet().iterator(); //реинициализируем первый итератор
                first.next(); // шаг вперёд
                first.remove(); // удаляем первый итератор (он же был в совпадениях)
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
        HashMap myMap = createMap();
        removeTheFirstNameDuplicates(myMap);
    }
}
