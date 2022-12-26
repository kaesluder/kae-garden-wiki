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

## React Idioms

```JavaScript
// test if rendered object has two nodes matching id
expect(await screen.findAllByTestId('WorldTimeEdit')).toHaveLength(2);

// test if callback function is called
const setter = jest.fn();
expect(setter).toHaveBeenCalledTimes(1);

// test if object has class
expect(hiddenInput).toHaveClass('state-display');

// test for text display
expect(screen.getByText('Hello, World!')).toBeInTheDocument();
// regex
expect(screen.getByText(/Eastern/)).toBeInTheDocument();

```

## Links

* [Testing local storage with testing library](https://plainenglish.io/blog/testing-local-storage-with-testing-library-580f74e8805b)
