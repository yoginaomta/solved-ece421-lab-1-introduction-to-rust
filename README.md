Download Link: https://assignmentchef.com/product/solved-ece421-lab-1-introduction-to-rust
<br>



<ul>

 <li>Introduction to Rust programming</li>

 <li>Getting up and running with Rust</li>

 <li>Running your first Rust program</li>

 <li>Add dependencies to your project</li>

 <li>Experiment with arithmetic libraries in Rust.</li>

</ul>

<strong>What is Rust? </strong>

<ul>

 <li>Rust is a multi-paradigm system programming, focused on safety, speed, and concurrency.</li>

 <li>Rust supports a mixture of imperative procedural, concurrent actor, object-oriented, and pure functional styles.</li>

 <li>It also supports generic programming and metaprogramming, in both static and dynamic styles.</li>

 <li>The syntax is similar to C++.</li>

 <li>The compiler is free and open-source software.</li>

</ul>

<strong>Getting Started with Rust </strong>

<ul>

 <li>You can try Rust online in the <u>Rust Playground</u>.</li>

 <li>Alternatively, you can install Rust using the Rustup tool, which is a Rust installer and version management tool.

  <ul>

   <li>On Linux and macOS systems, this is done as:</li>

  </ul></li>

</ul>

$ curl https://sh.rustup.rs -sSf | sh

<ul>

 <li>On windows, install <u>rustup-init.exe</u>.</li>

</ul>

<ul>

 <li>When you install <em>Rustup</em>, you will also get the latest stable version of the Rust build tool and package manager, also known as <strong><em>Cargo</em></strong>.</li>

 <li><strong>Editors:</strong> Rust support is available in many editors such as Sublime, IntelliJ IDEA, and Eclipse.</li>

</ul>

<strong>What is Cargo? </strong>

<ul>

 <li>Cargo is a tool that allows Rust packages to declare their various dependencies and ensure that you’ll always get a repeatable build.</li>

 <li>To accomplish this goal, Cargo does four things:

  <ul>

   <li>Introduces two metadata files with various bits of package information. o Fetches and builds your package’s dependencies.</li>

   <li>Invokes <em>rustc</em> or another build tool with the correct parameters to build your package.</li>

   <li>Introduces conventions to make working with Rust packages easier.</li>

  </ul></li>

</ul>




<h1>Deliverable 1: Writing your First Package with Cargo</h1>

<ul>

 <li>To create a new package, you can use <em>cargo new</em>:</li>

</ul>

$ cargo new hello_world

<ul>

 <li>Cargo has generated a new directory hello-rust with the following files:</li>

</ul>

hello-rus

├── Cargo.toml

└── src

└── main.rs

1 directory, 2 files

o <em>Cargo.toml: </em>is the manifest file which keeps metadata for the project along with the dependencies. o <em>src/main.rs</em> is where you write your code.

<ul>

 <li>Here’s what you’ll find in <em>src/main.rs</em>:</li>

</ul>

fn main() {     println!(“Hello, world!”); }

<ul>

 <li>To compile your project, we’ll use Cargo:</li>

</ul>

$ cargo build

<ul>

 <li>And then run it:</li>

</ul>

$ cargo run

<ul>

 <li>You can also use Cargo to:</li>

</ul>

o build a project with cargo build o run a project with cargo run o test a project with cargo test o create documentation with cargo doc o publish a project as a library (crate) with cargo publish

<ul>

 <li><strong>DEMO this deliverable to the lab instructor. </strong></li>

</ul>

<strong>             </strong>

<h1>Deliverable 2: Adding dependencies</h1>

<ul>

 <li>Now, let us add a dependency to our project.</li>

</ul>

Rust stores all sorts of libraries on <u>crates.io</u>. <em>Crates</em> are what you use to refer to packages.

<ul>

 <li>In this part of the lab, we will use a crate called <u>Rand</u>, which is a Rust library for random number generation (<strong>Hint</strong>: this library may come handy with any randomness-related algorithms)</li>

 <li>To add the crate to our project, we need to modify the <em>toml</em> file as follows:</li>

</ul>

[dependencies] rand = “0.7.0”

<ul>

 <li>You can find this information on from the crate page</li>

 <li>Now we run to let Cargo install the dependency:</li>

</ul>

cargo build

<ul>

 <li>Note that running this command creates a new file, <em>lock</em>, which is the log for the versions of the dependencies we are using.</li>

 <li>To actually use Rand in your code, you need to open main.rs and modify it as follows:</li>

</ul>

<table width="639">

 <tbody>

  <tr>

   <td width="639">use rand::prelude::*; fn main() {     let mut rng = thread_rng();     if rng.gen() {          let x: f64 = rng.gen();          let y = rng.gen_range(-10.0, 10.0);         println!(“x is: {}”, x);         println!(“y is: {}”, y);println!(“Random Number between 0 and 9: {}”, rng.gen_range(0, 10));}}</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>The first line imports everything from the prelude which is the lazy way to use rand as it only imports the most common items.</li>

</ul>

The Rand library automatically initializes a thread-local generator which can be accessed via the <em>thread_rng</em> and random functions. For more information, see <u>this link</u>.

<ul>

 <li><strong>DEMO this deliverable to the lab instructor. </strong></li>

</ul>

<strong>     </strong>

<h1>Deliverable 3: The Mathematics of Cryptology</h1>

Nearly all modern systems use cryptography as an important tool. At the hearty of cryptography are prime numbers, a prerequisite in a public-key system is the efficient generation of public-key parameters.

For instance, cryptosystems require <em>prime numbers</em> p and q for an admissible RSA modulus <strong><em>n = pq</em></strong>.

Many cryptosystems depend on a trapdoor one-way function, which is a mathematical function that is easy to compute in one way but requires secret information to compute efficiently its inverse. We can construct trapdoors one-way functions from hard number-theoretic problems like the integer factorization. The formal definition of factoring is:

Given a composite integer N, the factoring problem is to find integers p, q such that pq=N.

So far, the largest number factored is 232 digits long (768-bit) by using hundreds of computers and two years. Using a home computer, it would have taken 2000 years. Finding the prime factors for numbers the size of what we use for cryptography today (2048 bits) it is approximately four billion times harder than 768-bits.

Before starting to generate prime numbers, we need to select an arbitrary-precision arithmetic library. This is required; because the numbers that we are going to manipulate might be pretty big (a 1024-bit number is an integer of 309 digits). It is needed to use a special data structure to support big integers. Usually, the Integer class manages 32 bits, meaning it can hold values up to 2³² (4,294,967,295) which for many applications might be enough; however, to achieve security we need to be able to use big numbers. We do not just need to store the numbers, but to compute operations like multiplications and exponentiations between them. Rust has (many) common arbitrary-precision arithmetic libraries, e.g., <u>rug</u>, <u>apint</u>.

fn function(n: u32) -&gt; Int  {     let mut rng = rand::thread_rng();     loop {         let mut candidate:Int = Int::from(rng.gen_range(0, n));          candidate.set_bit(0, true);         let i = u64::from(&amp;candidate);         if is_prime(i)== true {              return candidate;

}

}

}

<strong>Question 1.</strong> What is the above algorithm doing?

<strong>Question 2.</strong> Rewrite the above algorithm to use another multiple-precision arithmetic library (e.g., rug, apint).

<ul>

 <li>To test whether a number is prime or not, there is the school method which is to iterate over all the smaller numbers and check if any of those numbers perfectly divide the prime candidate. We can immediately optimize our first attempt. First of all, we do not need to iterate through all the numbers, but just up to the square root, (the random number is forced to be odd). A better approach is to use a probabilistic algorithm, which can be used to determine whether a number is prime with a given degree of confidence. Probabilistic algorithms are algorithms that employ randomness to reduce the complexity or expected running time. The most known probabilistic algorithm used in practice is the Miller-Rabin test. It determines whether a candidate number is prime or not. The confidence of the algorithm depends on the number of iterations. Three iterations lead to a probability of failing to once in 2⁸⁰, which is considered a secure implementation.</li>

</ul>

<table width="639">

 <tbody>

  <tr>

   <td width="639">fn miller_rabin(candidate: &amp;Int) -&gt; bool {     let (s, d) = rewrite(candidate);     for _ in 0..5 {         let basis = thread_rng().gen_int_range(&amp;Int::from(2), candidate);         let mut x = mod_exp(&amp;basis, &amp;d, candidate);         if x == 1_usize || x == (candidate – 1_usize) {             continue;         } else {             for _ in Int::one()..s – 1_usize {                 x = mod_exp(&amp;x, &amp;Int::from(2), candidate);                 if x == 1_usize {                     return false;} else if x == candidate – 1_usize {break;}}             return false;}    }     true}</td>

  </tr>

 </tbody>

</table>

<strong>Question 3.</strong> Explain the algorithm the above code segment is implementing.

<strong>Question 4.</strong> Several cryptographic libraries use the Miller-Rabin test to output probable primes. <u>Albrecht et al</u>. were able to construct composite numbers that some of these libraries declared to be prime. Hence, we need something better. Identify the carte which most closely implements the recommendations from Prime and Prejudice.

<strong>Question 5.</strong>  Finally, prime fun. Prime number 41, can be written as the sum of six consecutive prime numbers: 41 = 2 + 3 + 5 + 7 + 11 + 13

This is the longest sum of consecutive primes that adds to a prime below one-hundred.

The longest sum of consecutive primes below one-thousand that adds to a prime contains X terms and is equal to Y. Write a Rust program which calculates and prints X, Y, and the list of primes.