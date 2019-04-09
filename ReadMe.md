As requested, here is a very basic example of unit testing to help you familiarize yourself with the topic and get all of us on the same page! This is a basic walkthrough following the tutorial at https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-dotnet-test.
------------------------------------------------
## Creating the source project

- In a completely empty folder in VSCode, create a directory called *unit-testing-using-dotnet-test* to hold the solution and change the path to this directory.

- Inside this new directory, run `dotnet new sln`.

- Inside the solution directory, create a *PrimeService* directory.

- Change the path to the *PrimeService* directory.

- Inside this new directory, run `dotnet new classlib`.

- Rename *Class1.cs* to *PrimeService.cs*. You will first create a failing implementation of the PrimeService class.
```
using System;

namespace Prime.Services
{
    public class PrimeService
    {
        public bool IsPrime(int candidate)
        {
            throw new NotImplementedException("Please create a test first");
        }
    }
}
```

- Change the directory back to the *unit-testing-using-dotnet-test* directory.

- Run the `dotnet sln add ./PrimeService/PrimeService.csproj` command to add the class library project to the solution.

## Creating the test project

- Next, create a *PrimeService.Tests* directory. 

- Change the directory to the the *PrimeService.Tests* directory. 

- Create a new project using `dotnet new xunit`.

- Add the PrimeService class library as another dependency to the project using `dotnet add reference ../PrimeService/PrimeService.csproj`

- Change the directory to the *unit-testing-using-dotnet-test* directory.

- Run the following command `dotnet sln add ./PrimeService.Tests/PrimeService.Tests.csproj`.

## Creating the first test

- You write one failing test, make it pass, then repeat the process. Remove *UnitTest1.cs* from the *PrimeService.Tests* directory and create a new C# file named *PrimeService_IsPrimeShould.cs*. Make sure the code in *PrimeService_IsPrimeShould.cs* is exactly the code below.
```
using Xunit;
using Prime.Services;

namespace Prime.UnitTests.Services
{
    public class PrimeService_IsPrimeShould
    {
        private readonly PrimeService _primeService;

        public PrimeService_IsPrimeShould()
        {
            _primeService = new PrimeService();
        }

        [Fact]
        public void ReturnFalseGivenValueOf1()
        {
            var result = _primeService.IsPrime(1);

            Assert.False(result, "1 should not be prime");
        }
    }
}
```

- From the *PrimeService.Tests* folder, execute `dotnet test` to build the tests and the class library and then run the tests.

- Your test should fail because you haven't created the implementation yet. Make this test pass by writing the simplest code in the PrimeService class that works. Replace the existing IsPrime method implementation in the *PrimeService.cs* file with the code below.
```
public bool IsPrime(int candidate)
{
    if (candidate == 1)
    {
        return false;
    }
    throw new NotImplementedException("Please create a test first");
}
```

- In the *PrimeService.Tests* directory, run `dotnet test` again. The dotnet test command runs a build for the PrimeService project and then for the PrimeService.Tests project. After building both projects, it runs this single test. It passes.

