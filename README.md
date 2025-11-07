# Crypto-market-calculator-
def calculate_pnl(entry_price, exit_price, position_size, leverage, position_type):
    crypto_amount = position_size / entry_price

    if position_type.lower() == "long":
        pnl = (exit_price - entry_price) * crypto_amount
    elif position_type.lower() == "short":
        pnl = (entry_price - exit_price) * crypto_amount
    else:
        raise ValueError("Position type must be 'long' or 'short'.")

    # Return on Investment
    initial_margin = position_size / leverage
    roi = (pnl / initial_margin) * 100

    return pnl, roi


def main():
    print("🔢 Crypto Futures PnL Calculator with Multiple Trades")

    total_pnl = 0
    total_roi = 0
    trade_count = 0

    while True:
        print("\n📥 Enter trade details:")
 try:
            entry_price = float(input("➤ Entry Price (INR): "))
            exit_price = float(input("➤ Exit Price (INR): "))
            position_size = float(input("➤ Position Size (in INR): "))
            leverage = float(input("➤ Leverage: "))
            position_type = input("➤ Position Type (long/short): ").strip().lower()
        except ValueError:
            print("⚠️ Invalid input. Please enter numeric values.")
            continue

        pnl, roi = calculate_pnl(entry_price, exit_price, position_size, leverage, position_type)

        # Update totals
        total_pnl += pnl
        total_roi += roi
        trade_count += 1

        print(f"\n✅ Trade {trade_count} Results:")
        print(f"• PnL: {pnl:.2f} INR")
        print(f"• ROI: {roi:.2f}%")

        # Ask to continue or finish
        cont = input("\n➕ Add another trade? (yes/no): ").strip().lower()
        if cont not in ("yes", "y"):
            break

    # Final Summary
    avg_roi = total_roi / trade_count if trade_count > 0 else 0
    print("\n📊 Final Summary:")
    print(f"• Total Trades: {trade_count}")
    print(f"• Total PnL: {total_pnl:.2f} INR")
    print(f"• Average ROI: {avg_roi:.2f}%")
if __name__ == "__main__":
    main()
