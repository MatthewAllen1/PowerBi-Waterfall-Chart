This waterfall chart took a lot of effort to show the change from last year to this year. PowerBi limits you to only showing a total instead of showing LY to TY. For privacy issues, I can't show my work exactly but I can show the final screenshot/product. For a reference I used this link to show the concept of creating something like this: https://businessintelligist.com/2020/06/12/power-bi-dax-how-to-make-waterfall-charts-work-showing-starting-and-ending-values/

First you have to create your tables and create a calc with switch functions to pull each row from the tables. By using the switch function you can get a waterfall chart to show TY and LY instead of total. Very nice.
Example calc:
PVM (Margin) Bridge =
SWITCH (
    SELECTEDVALUE ( Walk[WalkSort] ),
    1, SWITCH (
        SELECTEDVALUE ( PVM[PVM] ),
        “Price”, -1 * [PVM Margin – Price Impact],
        “Volume”, -1 * [PVM Margin – Volume Impact],
        “Mix”, -1 * [PVM Margin – Mix Impact],
        [Margin LY]
    ),
    2, SWITCH (
        SELECTEDVALUE ( PVM[PVM] ),
        “Price”, 0,
        “Volume”, 0,
        “Mix”, 0,
        [Margin]
    )
)
