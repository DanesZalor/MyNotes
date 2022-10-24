### Iteration 1 
```C#
new Prompt("Airline Reservation System", 
    new (string, Prompt)[]
    {
        ("Flight Maintenance", 
            new (string, Action)[]
            {
                ("Add Flight",    () => { /*ADD FLIGHT*/ } )
                ("Search Flight", () => { /*SEARCH FLIGHT*/} ) 
            }
        ),("Reservations", 
            /*Something*/
        )
    }
)
```
Ok but very confusing

### Iteration 2
```C#
class Prompt
{
    public readonly string _promptMsg;
    public readonly (string, Prompt)[] _choices;

    public Prompt(string promptMsg, params (string, Prompt)[] choices)
    {
        if(choices.Length == 0)
        {
            throw new ArguementException();
        }

        _promptMsg = promptMsg;
        _choices = choices;
    }

    private int getUserInputWithinChoicesRange() // 1-based
    {
        string? userInput = Console.ReadLine();

        if (
            (userInput == null) || (userInput.Length == 0) || 
            (!int.TryParse(userInput, out int parsedInput)) || 
            (parsedInput < 1 || parsedInput > _choices.Length)
        ) {
            throw new ArgumentOutOfRangeException("userInput", $"Must be 1-{_choices.Length}");
        }

        return parsedInput;
    } 

    public void Execute()
    {
        if(_choices.Length == 1)
    }
}
```