# Swimming-Pool-Ticket-
// Mengimpor readline untuk menerima input dari keyboard
import * as readline from "readline";

// Membuat interface input dan output terminal
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

// Menyimpan nilai tetap diskon member sebesar 10%
const MEMBER_DISCOUNT: number = 0.1;

// Menyimpan data yang digunakan program
let memberStatus: string = "";
let isMember: boolean = false;
let dayChoice: number = 0;
let categoryChoice: number = 0;
let price: number = 0;
let discount: number = 0;
let totalPayment: number = 0;

// Meminta status member
rl.question("Are you a member? (yes/no): ", (memberInput) => {
  memberStatus = memberInput;
  isMember = memberStatus === "yes";

  // Menampilkan pilihan hari
  console.log("\n=== SELECT DAY ===");
  console.log("1. Weekday - Rp20000");
  console.log("2. Weekend - Rp30000");
  console.log("3. Holiday - Rp40000");

  // Meminta pilihan hari
  rl.question("Choose a day (1-3): ", (dayInput) => {
    dayChoice = Number(dayInput);

    // IF 1: hanya menerima pilihan hari 1, 2, atau 3
    if (dayChoice === 1 || dayChoice === 2 || dayChoice === 3) {
      // SWITCH 1: menentukan harga berdasarkan hari
      switch (dayChoice) {
        case 1:
          price = 20000;
          break;

        case 2:
          price = 30000;
          break;

        case 3:
          price = 40000;
          break;

        default:
          break;
      }

      // Menampilkan pilihan kategori
      console.log("\n=== VISITOR CATEGORY ===");
      console.log("1. Child");
      console.log("2. Student");
      console.log("3. Adult");

      // Meminta pilihan kategori
      rl.question("Choose a category (1-3): ", (categoryInput) => {
        categoryChoice = Number(categoryInput);

        // IF 2: hanya menerima kategori 1, 2, atau 3
        if (
          categoryChoice === 1 ||
          categoryChoice === 2 ||
          categoryChoice === 3
        ) {
          // SWITCH 2: menentukan potongan berdasarkan kategori
          switch (categoryChoice) {
            case 1:
              price -= 5000;
              break;

            case 2:
              price -= 3000;
              break;

            case 3:
              price += 0;
              break;

            default:
              break;
          }

          // IF 3: member mendapat diskon jika harga minimal Rp30000
          if (isMember && price >= 30000) {
            discount = price * MEMBER_DISCOUNT;
          }

          // IF 4: memastikan harga valid
          if (price > 0) {
            totalPayment = price - discount;

            // Menampilkan hasil akhir
            console.log("\n=== SWIMMING POOL TICKET ===");
            console.log("Price: Rp" + price);
            console.log("Member Discount: Rp" + discount);
            console.log("Total Payment: Rp" + totalPayment);
          }
        } else {
          console.log("Invalid visitor category.");
        }

        // Menutup readline
        rl.close();
      });
    } else {
      console.log("Invalid day choice.");
      rl.close();
    }
  });
});
