# Editing a JSON file with vim
> NOTE: Make a copy of this file before modifying it.
Press '6G' to start

## Move between objects
1. Move to next bracket                                 ]]
2. Move between the corresponding bracket and back      %%
3. Move to next level array                             /[<cr> 
4. Move to next object                                  /{<cr>
5. Move to next object                                  n
{
    "key1": {
        "key2": "value2"
    },
    "key3": [
        {
            "key4": "value4"
        },
        {
            "key5": "value5"
        }
    ]
}

## Remove object
1. Move to 'key6'                                       /key6<cr>n
2. Remove entire object                                 Va{d
3. Restore object                                       u
4. Remove everything inside array                       di[
5. Paste removed object back                            P
[
    {
        "key6": "value6"
    },
    {
        "key7": "value7"
    }
]