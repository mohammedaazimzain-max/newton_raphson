#include <iostream>
#include <vector>
#include <cmath>

using namespace std;

// Draw a filled triangle recursively
void drawTriangle(vector<string>& canvas,
                  int x, int y,
                  int size)
{
    if (size <= 1)
    {
        canvas[y][x] = '*';
        return;
    }

    int half = size / 2;

    // Top triangle
    drawTriangle(canvas, x, y, half);

    // Bottom-left triangle
    drawTriangle(canvas, x - half, y + half, half);

    // Bottom-right triangle
    drawTriangle(canvas, x + half, y + half, half);
}

int main()
{
    int order;

    cout << "Enter recursion order (1-8 recommended): ";
    cin >> order;

    if (order < 1)
    {
        cout << "Order must be at least 1.\n";
        return 0;
    }

    int height = 1 << order;        // 2^order
    int width = height * 2 - 1;

    vector<string> canvas(height, string(width, ' '));

    drawTriangle(canvas, width / 2, 0, height);

    for (const auto& row : canvas)
        cout << row << '\n';

    return 0;
}
