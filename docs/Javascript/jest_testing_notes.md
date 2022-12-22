# Jest testing notes

## Use async/await to handle events and rendered results in react. 

```JavaScript

  test('edit form triggers setter function', async () => {
    const setter = jest.fn();

    render(<PageHeading pageHeadingState="Hello, World!" setter={setter} />);
    const hiddenInput = screen.getByTestId('headerEdit');
    await fireEvent.keyDown(hiddenInput, {
      key: 'Enter',
      code: 'Enter',
      charCode: 13,
    });
    expect(setter).toHaveBeenCalledTimes(1);
  });

```

## Links

* [Testing local storage with testing library](https://plainenglish.io/blog/testing-local-storage-with-testing-library-580f74e8805b)
