package kodut55;

import java.util.Random;
import java.util.Scanner;

public class Kakskend1 {
	
	

	private static Scanner scanner = new Scanner(System.in);
	Scanner keyboard = new Scanner(System.in);

	// !!! ESIMENE OSA - PANUSTE SISESTAMINE !!!!!
	public static void main(String[] args) {
		new Kakskend1().run();
	}

	public void run() {

		
		int raha;
		int panus;
		boolean kasutajav5it;

		System.out.println("Tere tulemast mängu BlackJack");
		System.out.println();

		raha = 100; // alguses on 100 ühikut raha

	//Panuse sisestus mängu alguses
		while (true) {
			System.out.println("Sul on " + raha + " eurot.");
			do {

				System.out
						.println("Mitu eurot tahad panustada (Vajuta 0, et katkestada)");

				panus = keyboard.nextInt();
				if (panus < 0 || panus > raha) {
					System.out.println("Sinu panus peab jääma vahemikku 0 ja "
							+ raha + ".");
				} //Kirjeldus käesoleva raha ja panuse suhted kui võidad/kaotad
			} while (panus < 0 || panus > raha);
			if (panus == 0) {
				raha = raha + panus;
				break;
			}
			kasutajav5it = Blackjack();
			if (kasutajav5it) {
				raha = raha + panus;
			} else {
				raha = raha - panus;
			} //Kui raha == 0; lõpetab programm töötamise 
			System.out.println();
			if (raha == 0) {
				System.out.println("Sinu rahakott on tühi!");
				break;
			}
		}

		System.out.println();
		System.out.println("Lahkud mängust " + raha + " euroga.");
	}
	// !!! ESIMENE OSA - PANUSTE SISESTAMINE LÕPP !!!!!
	
	// !!! TEINE OSA - KAARTIDE KIRJELDUS !!!!!
	
	//Kaartide kirjeldused (kaartid alates 10 on pildiga kaartid)
	private boolean Blackjack() {

		Scanner keyboard = new Scanner(System.in);

		int[] uusKaart = { 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 6,
				6, 6, 6, 7, 7, 7, 7, 8, 8, 8, 8, 9, 9, 9, 9, 10, 10, 10, 10,
				10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 11, 11, 11, 11 };
		// !!! TEINE OSA - KAARTIDE KIRJELDUS LÕPP???!!!!!
		
		
		// !!! KOLMAS OSA - MÄNG ISE, KAARTID KÄES JUBA !!!!!
		
		shuffleArray(uusKaart);
	//Esimesed kättejagatud kaartid MÄNGIJAL
		System.out.println();
		System.out.println("Sinu kaardid on: " + uusKaart[0] + " ja "
				+ uusKaart[1] + ".");
		int mKogusumma = uusKaart[0] + uusKaart[1];
		System.out.println("Sinu kogusumma on: " + mKogusumma + ".");
		System.out.println();

		//Kirjeldus esimeses roundis võimaliku blackjacki/lõhki minemise kohta
		if (mKogusumma == 21) {
			System.out.println("BLACKJACK, sinu võit!");
			return true;
		}
		if (mKogusumma > 21) {
			System.out.println("Lõhki, kaotasid!");
			return false;
		}
		//Esimese roundi kaartid DIILERIL ja kirjeldus selle kohta, kas on lõhki või blackjack (
		System.out.println("Diileril on: " + uusKaart[2]
				+ " ja varjatud kaardid");
		int dKogusumma = uusKaart[2] + uusKaart[3];
		if (dKogusumma > 21) {
			System.out.println();
			System.out.println("Diileri kogusumma on: " + dKogusumma + ".");
			System.out.println("Diiler läks lõhki, sinu võit!");
			return true;
		}
		if (dKogusumma == 21) {
			System.out.println();
			System.out.println("Diiler paljastab oma teise kaardi: "
					+ uusKaart[3] + ".");
			System.out.println("Diileri kogusumma on: " + dKogusumma + ".");
			System.out.println();
			System.out.println("Diileril on BLACKJACK, kaotasid!");
			return false;
		}
		System.out.println("Tema kogusumma on peidetud!");
		System.out.println();

		// Kui esimene round ei l6ppenud blackjacki või l6hkiminekuga, siis kas "juurde" või "l6pp".
		// "l6pp" on siin kirjeldamata, proovisin, kuid lõi programmi sassi. Seega pärast 
	    //  esimest roundi "l6pp" ei tööta praegu.
	
		

		System.out.print("Tahad kaarte \"juurde\" või \"l6pp\"? ");
		String hitStay = keyboard.next();
		System.out.println();

		// cc = kaartide arv
		int cc = 4;
		if (hitStay.equalsIgnoreCase("juurde")) {

			while (mKogusumma < 21 && hitStay.equalsIgnoreCase("juurde")) {
				if (hitStay.equalsIgnoreCase("juurde")) {
					System.out.println("Sa tõmbasid: " + uusKaart[cc] + ".");
					mKogusumma = mKogusumma + uusKaart[cc];
					System.out
							.println("Sinu kogusumma on: " + mKogusumma + ".");
					System.out.println();
					cc++;
// Kirjeldus: kas p2rast juurde v6tmist l2ksid lõhki või said BLACKJACKI. 
					// Kui mitte kumbki, siis saad võtta juurde
					if (mKogusumma > 21) {
						System.out.println("Läksid lõhki, kaotasid!");
						return false;
					}
					if (mKogusumma == 21) {
						System.out.println("BLACKJACK, sinu võit!");
						return true;
					}
					System.out.print("Tahad kaarte \"juurde\" või \"l6pp\"? ");
					hitStay = keyboard.next();
					System.out.println();

					// Kuna "juurde" on juba eelnevalt kirjeldatud, siis seekord kirjeldasin "l6pp"
					// Seekord t55tavad nii l6pp kui juurde, viga ei oska 5elda.
					if (hitStay.equalsIgnoreCase("l6pp")) {

						while (mKogusumma < 21
								&& hitStay.equalsIgnoreCase("l6pp")) {
							if (hitStay.equalsIgnoreCase("l6pp")) {
								System.out
										.println("Sa ei võtnud kaarte juurde");

								System.out.println("Sinu kogusumma on: "
										+ mKogusumma + ".");
								System.out.println("Diileri kogusumma on: "
										+ dKogusumma + ".");
								System.out.println();
								cc++;

								if (mKogusumma > 21) {
									System.out
											.println("Läksid lõhki, kaotasid!");
									return false;
								}
								if (mKogusumma == 21) {
									System.out.println("BLACKJACK, sinu võit!");
									return true;
								}
								if (mKogusumma == dKogusumma) {
									System.out.println("VIIK");
									return true;

								}
								if (mKogusumma < 21 && mKogusumma > dKogusumma) {
									System.out.println("SINU VÕIT");
									return true;

								}
								if (mKogusumma < 21 && mKogusumma < dKogusumma) {
									System.out.println("KAOTASID");
									return false;

								}
							}

						}

						// !!! KOLMAS OSA - MÄNG ISE, KAARTID KÄES JUBA !!!!! 						
						// Kui koodi vaadata, siis see osa tuleb täpselt nii jube pikk
						// Samas, see osa mis nüüd siia alla jääb, oleks ka imelik, kui välja jääb.
						// Võib-olla siis meetod kuni kommentaarini // Lõplik kokkuvõte?!
						
						keyboard.close();
						System.out.println("Diileri kord");
						System.out.println("Tema peidetud kaart on: "
								+ uusKaart[3] + ".");

						cc++;
						while (dKogusumma < 16) {
							System.out.println();
							System.out.println("Diiler võtab juurde.");
							System.out.println("Ta tõmbab: " + uusKaart[cc]
									+ ".");
							cc++;
							dKogusumma = dKogusumma + uusKaart[cc];
							System.out.println();
							System.out.println("Tema kogusumma on: "
									+ dKogusumma);

							if (dKogusumma > 21) {
								System.out.println();
								System.out
										.println("Diiler läks lõhki, sinu võit!");
								return true;
							}

							if (dKogusumma < 21 && dKogusumma > 16) {
								System.out.println();
								System.out.println("Diiler passib.");
							}
						}

						// Lõplik kokkuvõte - see ka eraldi meetodina!?
						System.out.println();
						System.out.println("Diileri kogusumma on: "
								+ dKogusumma);
						System.out.println("Sinu kogusumma on: " + mKogusumma);
						System.out.println();

						if (dKogusumma > mKogusumma) {
							System.out.println("Diiler võitis!");
						}
						if (dKogusumma == mKogusumma) {
							System.out.println("Viik!");

						}
						if (dKogusumma < mKogusumma) {
							System.out.println("Sinu võit!");

						}
					}
				}
			}
		}
		return false;
	}
// Pluss see eraldi meetodiks.
	static void shuffleArray(int[] deckCards) {

		Random rnd = new Random();
		for (int i = deckCards.length - 1; i > 0; i--) {
			int index = rnd.nextInt(i + 1);
			// vahetus
			int a = deckCards[index];
			deckCards[index] = deckCards[i];
			deckCards[i] = a;
		}
	}
}
