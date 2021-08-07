    输入：
    goudan2 60 80 80
    zhaowu 60 80 80
    zhangsan 60 80 80
    yatou 90 80 80
    goudan1 60 80 80
    gousheng 80 100 60
    lilei 80 100 60
    hanmingmei 80 90 60
    liutao 80 100 60
    SimonYin 80 100 60
    
    输出：首先排除小于60分的；其次列出总分排名前三的
    [First round name list]
    yatou 90 80 80
    SimonYin 80 100 60
    gousheng 80 100 60
    lilei 80 100 60
    liutao 80 100 60
    hanmingmei 80 90 60
    goudan1 60 80 80
    goudan2 60 80 80
    zhangsan 60 80 80
    zhaowu 60 80 80
    
    [Final name list]
    yatou 90 80 80
    SimonYin 80 100 60
    gousheng 80 100 60
    lilei 80 100 60
    liutao 80 100 60
    hanmingmei 80 90 60
    
    
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        List<String> nameList = new ArrayList<>();
        List<Integer> sumGrades = new ArrayList<>();
        Map<Integer,ArrayList<String[]>> map = new HashMap<>();
        for(int i=0;i<10;i++){
            String s = in.nextLine();
            String[] strs = s.split(" ");
            String name = strs[0];
            Integer chinese = Integer.valueOf(strs[1]);
            Integer math = Integer.valueOf(strs[2]);
            Integer english = Integer.valueOf(strs[3]);
            if(chinese<60||math<60||english<60){
                continue;
            }
            nameList.add(name);
            int total = chinese+math+english;
            if(!sumGrades.contains(total)){
                sumGrades.add(total);
            }
            ArrayList<String[]> list = map.getOrDefault(total, new ArrayList<>());
            list.add(strs);
            map.put(total,list);
        }

        Collections.sort(nameList);
        Collections.sort(sumGrades,(i1,i2)->i2-i1);

        System.out.println("[First round name list]");
        for (Integer grade : sumGrades) {
            ArrayList<String[]> grades = map.get(grade);
            Collections.sort(grades, (o1, o2) -> {
                if(Integer.valueOf(o1[1])-Integer.valueOf(o2[1])!=0){
                    return Integer.valueOf(o2[1])-Integer.valueOf(o1[1]);
                }
                if(Integer.valueOf(o1[2])-Integer.valueOf(o2[2])!=0){
                    return Integer.valueOf(o2[2])-Integer.valueOf(o1[2]);
                }
                if(Integer.valueOf(o1[3])-Integer.valueOf(o2[3])!=0){
                    return Integer.valueOf(o2[3])-Integer.valueOf(o1[3]);
                }
                return nameList.indexOf(o1[0])-nameList.indexOf(o2[0]);   //按照姓名ASCII码
            });
            for (String[] strings : grades) {
                System.out.println(strings[0]+" "+strings[1]+" "+strings[2]+" "+strings[3]);
            }
            map.put(grade,grades);
        }

        System.out.println("[Final name list]");
        int index = 0;
        while(index<sumGrades.size()&&index<3){
            Integer grade = sumGrades.get(index);
            ArrayList<String[]> grades = map.get(grade);
            for (String[] strings : grades) {
                System.out.println(strings[0]+" "+strings[1]+" "+strings[2]+" "+strings[3]);
            }
            index++;
        }

    }
