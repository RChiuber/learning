# 數獨專案學習紀錄
## 數獨方格製作
- 再匯入方格時發現程式碼顯示-1經過與copilot討論之後發現是沒有main涵是以及宣告錯誤，導致顯示不出來
```c
#include <stdio.h>
void print_board(int board[][9]);
int main(){
    int board[9][9] = {
    {0, 0, 0, 0, 0, 0, 0, 9, 0},
    {1, 9, 0, 4, 7, 0, 6, 0, 8},
    {0, 5, 2, 8, 1, 9, 4, 0, 7},
    {2, 0, 0, 0, 4, 8, 0, 0, 0},
    {0, 0, 9, 0, 0, 0, 5, 0, 0},
    {0, 0, 0, 7, 5, 0, 0, 0, 9},
    {9, 0, 7, 3, 6, 4, 1, 8, 0},
    {5, 0, 6, 0, 8, 1, 0, 7, 4},
    {0, 8, 0, 0, 0, 0, 0, 0, 0}
};


    print_board(board);
    return 0;
}

void print_board(int board[][9]) {
    printf("\n +-------+-------+-------+\n");
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            if (j % 3 == 0) printf(" | ");
            else printf(" ");

            if (board[i][j] == 0) {
                printf("_");  // 用底線表示空格
            } else {
                printf("%d", board[i][j]);
            }
        }
        printf(" |\n");
        if (i % 3 == 2) printf(" +-------+-------+-------+\n");
    }
}
```
## 將盤面存到文字檔
- 經過以上的問題，這次成功宣告函式，並且理解其中的程式碼的功能
```c
#include <stdio.h>
void print_board(int board[][9]);
void save_to_text_file(int board[][9], const char* filename);
int main(){
    int board[9][9] = {
    {0, 0, 0, 0, 0, 0, 0, 9, 0},
    {1, 9, 0, 4, 7, 0, 6, 0, 8},
    {0, 5, 2, 8, 1, 9, 4, 0, 7},
    {2, 0, 0, 0, 4, 8, 0, 0, 0},
    {0, 0, 9, 0, 0, 0, 5, 0, 0},
    {0, 0, 0, 7, 5, 0, 0, 0, 9},
    {9, 0, 7, 3, 6, 4, 1, 8, 0},
    {5, 0, 6, 0, 8, 1, 0, 7, 4},
    {0, 8, 0, 0, 0, 0, 0, 0, 0}
};


    print_board(board);
    return 0;
}

void print_board(int board[][9]) {
    printf("\n +-------+-------+-------+\n");
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            if (j % 3 == 0) printf(" | ");
            else printf(" ");

            if (board[i][j] == 0) {
                printf("_");  // 用底線表示空格
            } else {
                printf("%d", board[i][j]);
            }
        }
        printf(" |\n");
        if (i % 3 == 2) printf(" +-------+-------+-------+\n");
    }
}
void save_to_text_file(int board[][9], const char* filename) {
    FILE *fp = fopen(filename, "w");
    if (fp == NULL) {
        printf("無法開啟檔案 %s 進行寫入\n", filename);
        return;
    }

    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            if (board[i][j] == 0) {
                fprintf(fp, ".");  // 使用點表示空格
            } else {
                fprintf(fp, "%d", board[i][j]);
            }
        }
        fprintf(fp, "\n");  // 每行結束換行
    }

    fclose(fp);
    printf("已成功儲存到 %s\n", filename);
}
```