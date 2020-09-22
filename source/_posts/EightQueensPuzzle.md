---
title: 八皇后问题
---
在8×8格的国际象棋上摆放八个皇后，使其不能互相攻击，即任意两个皇后都不能处于同一行、同一列或同一斜线上，问有多少种摆法。

```java

import java.util.Arrays;

/**
 * @author bwb
 * @date 2018/06/20
 */
public class Queen2 {

    private static int[] arr = new int[8];

    static int sum = 0;

    private static boolean check(int row) {
        for (int j = 0; j < row; j++) {
            if ((Math.abs(row - j)) == (Math.abs(arr[j] - arr[row])) // 在对角线上
                || (arr[j] == arr[row])) // 判断列号是否相同
                return false;
        }
        return true;
    }

    /**
     * 递归
     * @param row
     */
    private static void fun(int row) {
        if (row == 8) {
            int[][] a = new int[8][8];
            for (int i = 0; i < 8; i++) {
                a[i][arr[i]] = 1;
            }
            sum++;
            System.out.println(Arrays.deepToString(a));s
        } else {
            for (int col = 0; col < 8; col++) {
                arr[row] = col;
                if (check(row))
                    fun(row + 1);
            }
        }
    }

    public static void main(String[] args) {
        fun(0);
        System.out.println(sum);
    }

}

```
