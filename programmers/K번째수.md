# K번째수

## Source
[K번째수](https://school.programmers.co.kr/learn/courses/30/lessons/42748)


## Apporach

## Code
    import java.util.*;

    class Solution {
        public int[] solution(int[] array, int[][] commands) {
            List<Integer> list = new ArrayList<>();
            
            for(int[] command : commands){
                int[] tmp = new int[command[1] - command[0] + 1];
                int start = command[0]-1;
                int end = command[1];
            
                for(int i=start; i<end; i++){
                    tmp[i-start] = array[i];
                }
                
                Arrays.sort(tmp);
                
                list.add(tmp[command[2]-1]);
            }
            
            return list.stream().mapToInt(i->i).toArray();
        }
    }