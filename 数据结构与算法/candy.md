


        import java.util.Arrays;
        import java.util.Scanner;

        public class Candy {
        public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] q = new int[n];
        for (int i = 0; i < n; i++) {
            q[i] = sc.nextInt();
        }
        printQ(q);
        }

        public static void printQ(int[] q) {
        Arrays.sort(q);
        int sum = 0;//数组加和
        int avg = 0;//数组平均值
        int left = 0;//数组从左边的加和
        int right = 0;//数组从右边加和
        int midNum = 0;//中心数字
        //计算sum
        for (int i = 0; i < q.length; i++) {
            sum += q[i];
        }
        //计算avg
        avg = sum / 2;
        //数组从小到大加和（从左向右加和）
        for (int i = 0; i < q.length; i++) {
            left += q[i];
            //一旦加了a[i]大于avg了,记录a[i]
            if (left > avg) {
                midNum = q[i];
                left -= midNum;
                break;
            }
        }
        //相应的,a[i]右边的数加和
        right = sum - left - midNum;

        //计算结果（距离远的加上a[i],也就是midNum）
        int result1 = distance(left, right, avg, midNum);
        int result2 = sum - right;
        //判断两个数哪个大
        int maxOne = max(result1, result2);
        int minOne = min(result1, result2);
        System.out.println(minOne + "," + maxOne);
        }

        private static int min(int result1, int result2) {
        return (result1 < result2) ? result1 : result2;
        }

        private static int max(int result1, int result2) {
        return (result1 > result2) ? result1 : result2;
        }

        /**
        * 比较left 和 right哪个离avg更远，把midNum赋给更远的那个
        *
        * @param left
        * @param right
        * @param avg
        * @param midNum
        * @return
        */
        private static int distance(int left, int right, int avg, int midNum) {
        return (avg - left) >= (avg - right) ? (left + midNum) : (right + midNum);
        }
        }
