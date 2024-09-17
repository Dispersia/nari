Goals: [[Goals]]

fn main(args: [String]): i32 => {
	return 0;
}

fn factorial(n: i32): i32 = n match {
	0 => 1,
	 _ => n * factorial(n - 1)
}

const add = (a: i32, b: i32): i32 => a + b;

// WorkerThread is a channel
fn background_work(addition_function: (a: i32, b:i32): i32, a: i32, b: i32): WorkerThread\[Result\[i32, Error]] => {
	return add(a, b);
}

const do_work = background_work(add, 5, 10);

// Do Other Work

const work <- do_work

do_work -> match {
	Ok(num) => println(num),
	 Err(err) => eprintln(err)
}

// Example consuming multiple

var list: List\[Result\[i32, Error]] <- { do_work, do_work };
const list: List[i32] = list.filter(x => x.is_ok());