# 신입사원 이름 만들기

## 문제 
어떤 회사의 신입 사원 이름 목록이 제공됩니다. 각각의 신입사원에 대해 회사 이메일 주소를 생성해야 합 니다.
각 사람의 이름은 공백으로 구분된 '이름'(first name), '중간 이름' (middle name) (optional), '성'(last name)으로, 두가지 또는 세가지 조합으로 구성됩니다. 각 부분은 영어 대소문자로만 이루어져 있습니다 (단, '성'은 '-'(하이픈)문자가 포함될 수 있음). 회사 이름도 영문으로만 구성되어 있습니다.
각 주소는 "FirstMiddleLast@Company.com" 형식을 사용해야 합니다.
First는 '이름'의 이니셜,
Middle은 '중간 이름'의 이니셜(단, '중간 이름'이 있는 경우에만 해당),
Last는 '성'을 나타내며 최대 8개의 이니셜 문자로 잘립니다.
Company 는 회사 이름입니다.
주소는 소문자여야 하며 하이픈을 포함하지 않아야 합니다.
성을 자르기 전에 하이픈을 제거해야 합니다.
또한 두 명 이상의 사람이 동일한 이메일 주소를 사용하는 경우 "@" 기호 앞에 숫자(동일한 두번째 이메일 부터 숫자 2로 시작)를 추가하여 주소를 구분합니다. 예를 들어 주소가 "jd@company.com"인 사람이 3명 있는 경우 각각 "jd@company.com", "jd2@company.com" 및 "jd3@company.com" 주소를 할당받아야 합니다.
다음 함수를 작성하십시오:
class Solution { public String solution (String S, String C); }
", "(쉼표 다음에 공백) 문자로 구분된 이름 리스트 문자열 S, 회사 이름인 문자열 C가 함수 파라미터로 제 공됩니다. 반환 값으로는 입력(문자열 S)과 동일한 순서로", "문자로 구분된 "이름 <이메일>"형식의 리스 트 String을 반환합니다.
예를 들어, 주어진 C = "Example" 및 문자열 S는 다음과 같습니다:
"John Doe, Peter Parker, Mary Jane Watson-Parker, James Doe, John Elvis Doe, Jane Doe, Penny Parker"
함수는 다음을 반환해야 합니다:
"John Doe jdoe@example.com, Peter Parker pparker@example.com, Mary Jane Watson-Parker mjwatsonpa@example.com, James Doe jdoe2@example.com, John Elvis Doe jedoe@example.com, Jane Doe jdoe3@example.com, Penny Parker
pparker2@example.com".
다음과 같이 가정합니다:
문자열 S의 길이는 [3..1,000] 범위이다.
문자열 C의 길이는 [1..100] 범위이다.
문자열 S는 문자(a-z 및/또는 A-Z), 공백, 하이픈 및 쉼표로만 구성됩니다;
. 문자열 S에는 유효한 이름이 포함되어 있습니다. 이름이 두 번 이상 나타나지 않습니다.
. 문자열 C는 문자(a-z 및/또는 A-Z)로만 구성됩니다.
제출한 테스트의 정확성에 중점을 두어 검토합니다. 제출한 테스트의 성능(퍼포먼스)은 평가에 영향을 주 지 않습니다.

## 해답 

    public String makeEmail(String names, String domain) {
        String[] nams = names.split(", ");
        List<String> result = new ArrayList<>();
        HashMap<String, Integer> map = new HashMap<>();

        for (String name : nams) {
            String email = "";
            
            String[] parts = name.split(" ");

            for(int i=0; i<parts.length; i++) {
                if (i ==parts.length - 1) {
                parts[i] = parts[i].replaceAll("-", "");
                if(parts[i].length() > 8){
                    parts[i] = parts[i].substring(0, 8);
                }
                email += parts[i].toLowerCase();
                } else {
                email += Character.toLowerCase(parts[i].charAt(0));
                }
            }

            int count = map.getOrDefault(email, 0) + 1;
            map.put(email, count);
            if (count > 1 ){
                email += count  ;
            }
            email += domain;
            
            result.add(name + " <" + email+ ">");
        }  
        return String.join(", ", result);
    }