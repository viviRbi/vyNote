```javascript
import {StrengthPipe} from "./strength.pipe";

describe('StrengthPipe', () => {
	it('Should display weak if strength is 5', () => {
		let pipe = new StrengthPipe()

		expect(pipe.transform(5)).toEqual('5 (weak)');
	})
})

import { MessageService } from "./message.service"

des
```