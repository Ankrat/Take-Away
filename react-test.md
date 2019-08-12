# Generate the test folders

In an existing React app, creating the structure for snapshots might be cumbersome.

Running this snippet in the, let say `component` directory:
```sh
#!/bin/bash
LOCATION="."
for folder in "$LOCATION"/*; do
  [ -d "$folder" ] || continue
  mkdir -p "$folder/__tests__"
  touch "$folder/__tests__/$folder.test.js"
  fileName="${folder##*/}"
  componentName="$(tr '[:lower:]' '[:upper:]' <<< ${fileName:0:1})${fileName:1}"


echo "import React from 'react';
import { shallow } from 'enzyme';
import $componentName from '../$fileName.js';

describe('$componentName component', () => {
  let props;
  beforeEach(() => {
    props = {};
  });

  const getWrapper = () => shallow(<$componentName {...props} />);

  it('render without crashing', () => {
    expect(getWrapper()).toMatchSnapshot();
  });
});" > "$folder/__tests__/$folder.test.js"
done
```
