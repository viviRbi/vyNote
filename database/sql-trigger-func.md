```sql
------------------------------------------------------------------------------------------------------------------------------------------------------------------
----------------------------------------------------INSERT customer, bank account, employee, transaction name(type) DATA
insert into transaction_name(transaction_type) values ('deposit'),('withdraw'),('transfer');

insert into employee(username, password) values ('vy','vy');

insert into customer(username, password, birthday, phone, address, zipcode, state) values 
('Thanh','Le','1999-12-31','8322225687','19503 Salmon ln','45678','TX'),
('Lamba','Leila','1995-04-01','6657930596','44088 Alabama Dr','21906','TX');

insert into bank_account(rounting_number, account_number,balance) values 
(1,1,500),(2,2,7000), (3,2,3000);

insert into applied_bank_account(account_number,balance) values 
(1,500),(2,7000), (2,3000),(2,90);
delete from applied_bank_account where rounting_number <4;
------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------CREATE transaction table 
create table transaction (
	id serial primary key,
	create_at TIMESTAMP default now(), 
	transfer_amount decimal(19,2) default 0,
	transaction_name_id integer not null,
	foreign key (transaction_name_id) references transaction_name(id),
	--	if tranfer bank id(customer id) == null, that means they deposite
	transfer_customer_id integer,  
	--	if tranfered bank id(the 2nd customer id field) == null, that means they withdraw
	transfered_customer_id integer,
	foreign key (transfer_customer_id) references customer(id),
	foreign key (transfered_customer_id) references customer(id),
	transfer_bank_rounting integer,  
	transfered_bank_rounting integer,
	foreign key (transfer_bank_rounting) references bank_account(rounting_number),
	foreign key (transfered_bank_rounting) references bank_account(rounting_number)
);
create table pending_transaction (
	id serial primary key,
	create_at TIMESTAMP default now(), 
	transfer_amount decimal(19,2) default 0,
	transaction_name_id integer not null,
	foreign key (transaction_name_id) references transaction_name(id),
	transfer_customer_id integer,  
	transfered_customer_id integer,
	foreign key (transfer_customer_id) references customer(id),
	foreign key (transfered_customer_id) references customer(id),
	transfer_bank_rounting integer,  
	transfered_bank_rounting integer,
	foreign key (transfer_bank_rounting) references bank_account(rounting_number),
	foreign key (transfered_bank_rounting) references bank_account(rounting_number)
);
------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------CREATE TRIGGER FUNCTION for pending_transaction to delete itself after approved to transaction

-- If the transaction is in pending_transaction table, it already verified that user only transfer money to other user. Not his/her own account
create or replace function delete_pending_transaction()
	returns trigger as 
	$BODY$
	begin 
			delete from pending_transaction
			where pending_transaction.transfer_amount = new.transfer_amount
			and pending_transaction.transfer_bank_rounting = new.transfer_bank_rounting
			and pending_transaction.transfered_bank_rounting = new.transfered_bank_rounting
			and new.transaction_name_id = 3;
--		return null for delete. New = newly insert row on bank account
		return null;
	end;

	$BODY$
	language plpgsql;

create trigger delete_pending_transaction
after insert on transaction
for each row 
execute procedure delete_pending_transaction();
------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------CREATE TRIGGER FUNCTION for applied_bank_acount to delete itself after approved to bank_account
create or replace function delete_aprrove_applied_bank_account()
	returns trigger as 
	$BODY$
	begin 
			delete from applied_bank_account
			where applied_bank_account.rounting_number = new.rounting_number;
--		return null for delete. New = newly insert row on bank account
		return null;
	end;

	$BODY$
	language plpgsql;

create trigger delete_aprrove_applied_bank_account
after insert on bank_account 
for each row 
execute procedure delete_aprrove_applied_bank_account();

------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------CREATE TRIGGER FUNCTION for bank_acount when NEW transaction INSERTED (or update)
--add a trigger function to automaticaly 
--update bank_account when a transaction occur

create or replace function account_balance_change()
	returns trigger as 
	$BODY$
	begin  
			
	--		If deposite
			if new.transfer_bank_rounting IS null then
				update bank_account 
				set balance = balance + new.transfer_amount
				from transaction
				where bank_account.account_number = new.transfered_customer_id
				and bank_account.rounting_number = new.transfered_bank_rounting;
			end if;
		
--			if withdraw
			if new.transfered_bank_rounting IS null then
				update bank_account 
				set balance = balance - new.transfer_amount
				from transaction
				where bank_account.account_number = new.transfer_customer_id
				and bank_account.rounting_number = new.transfer_bank_rounting;
			end if;
		
--			if transfer
			if new.transfered_bank_rounting IS not null and new.transfer_bank_rounting IS not null then 
--				Giver
				update bank_account 
				set balance = balance - new.transfer_amount
				from transaction
				where bank_account.account_number = new.transfer_customer_id
				and bank_account.rounting_number = new.transfer_bank_rounting;
			
--				receiver
				update bank_account 
				set balance = balance + new.transfer_amount
				from transaction
				where bank_account.account_number = new.transfered_customer_id
				and bank_account.rounting_number = new.transfered_bank_rounting;
			end if;
		return new;
	end;

	$BODY$
	language plpgsql;

create trigger transaction_update_bank_balance
before insert or update on transaction 
for each row 
execute procedure account_balance_change();
```