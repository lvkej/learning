    输入
    This,is,an,eggplant,of,our,beautifull,sweety,baby
    16
    
    输出：
    This****is****an
    eggplant**of*our
    beautifull******
    sweety*baby*****
    
        public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        String s = in.nextLine();
        int l = in.nextInt();
        String[] strs = s.split(",");
        int left = 0, right = 0;

        while (left < strs.length) {
            int curLen = 0;
            while (curLen + strs[right].length() <= l) {
                curLen += strs[right].length() + 1;
                right++;
                if (right == strs.length) {
                    break;
                }
            }

            int word = right - left;    //一行的单词数
            int split = word == 1 ? 1 : word - 1;//一行的空格数
            String[] splits = new String[split];//每个空位*的个数
            int totalStar = curLen == l + 1 ? word - 1 : l - curLen + word;//总共*数

            if (right < strs.length) {
                int cnt = totalStar / split;
                String pre = "";
                for (int i = 0; i < cnt; i++) {
                    pre += "*";
                }
                Arrays.fill(splits, pre);
                int mod = totalStar % split;
                for (int i = 0; i < mod; i++) {
                    splits[i] = splits[i] + "*";
                }
            } else {
                Arrays.fill(splits, "*");
            }

            StringBuilder sb = new StringBuilder();
            if (word == 1) {
                sb.append(strs[left]);
                sb.append(splits[0]);
            } else {
                for (int index = left; index < right - 1; index++) {
                    sb.append(strs[index]);
                    sb.append(splits[index - left]);
                }
                sb.append(strs[right - 1]);
            }

            if (right == strs.length) {
                while (sb.length() < l) {
                    sb.append("*");
                }
            }
            System.out.println(sb.toString());
            left = right;
        }
    }
